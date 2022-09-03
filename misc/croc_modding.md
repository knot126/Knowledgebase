# Croc series modding notes

Notes:

 * **Not all of this information may be accurate.** Consider my [past](https://smashingtech.fandom.com/wiki/MTX) [RE work](https://smashingtech.fandom.com/wiki/LitMesh) before completely trusting this.
 * I am using the European PC release for Croc 2 and Croc DE 1.3.0 for Croc 1 as well as the EU demo of Croc 1 with debug symbols.

## Fixed point format

There seem to be three kinds of fixed point numbers used in Croc games: 16x16, 20x12 and 4x12.

To convert a float to a NxM fixed point value: `(int)(number * (2.0f ^ M))`

To convert a NxM fixed point value to a float: `(float)(number / (2.0f ^ M))`

Basically, you are just multiplying by the max number that M bits can represent plus one, therefore encoding the number with a fixed number of decimal places.

Here are a table of the types, for those that prefer examples:

| Type         | Size | Whole | Fractional | Max      | Step     | Magic Number     | Example To          | Example From         |
| ------------ | ---- | ----- | ---------- | -------- | -------- | ---------------- | ------------------- | -------------------- |
| 16x16        | 32   | 16    | 16         | ~65536   | ~0.00015 | 2^16 = 65536     | 1.5 * 65536 = 98304 | 98304 / 65536 = 1.5  |
| 20x12        | 32   | 20    | 12         | ~1048576 | ~0.0042  | 2^12 = 4096      | 1.5 * 4096 = 6144   | 6144 / 4096 = 1.5    |
| 4x12         | 16   | 4     | 12         | ~16      | ~0.0042  | 2^12 = 4096      | 2.0 * 4096 = 8128   | 8128 / 4096 = 2.0    |

----

### Sources

 * [crocutils: `libcroc/fixed.h`](https://github.com/vs49688/CrocUtils/blob/master/libcroc/include/libcroc/fixed.h)
 * [crocutils: `libcroc/fixeddef.h`](https://github.com/vs49688/CrocUtils/blob/master/libcroc/include/libcroc/fixeddef.h)

## Stratigies (Script) Information

There is a lot of information about strats in the Croc & Stuff discord server. I will try to note or link some places here for those that do not want to join a discord server just to see. Not much of this is original research by me.

### Virtual Machine

The virtual machine used to interpret the bytecode is [stack-based](https://en.wikipedia.org/wiki/Stack_machine). Roughly, that means that the operands to an operator are pushed onto the stack, then the operaton pops them and pushes the return value.

For example:

```asm
push 5      ; push 5 onto stack                                        - stack is [5]
push 11     ; push 11 onto stack                                       - stack is [5, 11]
mul         ; pop numbers [5, 11] and multiply, then push result       - stack is [55]
```

### Coroutines

While ASL has been thought to have been a coroutine-based language for a long time - mainly due to a reddit post - Nic Cusworth recently stated that it "definitely wasn't."

<details>
  <summary><i>Show original section</i></summary>
  
  It appears that the strategy system was highly coroutine based, so loops for example yeild back (return the entire function) unless they are told not to.
  
  As an example, think about trying to move the player by 10 every frame for 10 frames. Without coroutines, one would write:

  ```lua
  function update() {
  	if (frame < 10) {
  		player.position += 10;
  	}
  }
  ```
  
  With coroutines, it could be written like this:
  
  ```lua
  function update() {
  	updatePlayerPos();
  }
  
  function updatePlayerPos() {
  	while (frame < 10) {
  		player.position += 10;
  		yeild; -- returns control until called again, where it does another iteration
  	}
  }
  ```
</details>

### Dispatch

***WIP Documentation** research is mainly done on the Croc 1 demo on PSX right now, which seems like it does not always line up with the files in the retail game. (This would make sense, since the game was still being developed and strats were at their infancy, only being made for Croc 1.)*

Functions are dispatched (that is, found and run) based on a function pointer array. (It would be helpful to be fimilar with how [opcodes are read](http://craftinginterpreters.com/a-virtual-machine.html#executing-instructions) and [function pointers](https://www.learn-c.org/en/Function_Pointers).)

Each instruction has a related function in the game binary. These functions are stored in an array of type `stFunction`, where that type is defined as:

```c
typedef void (*stFunction)(stStrat *strat);
```

Which is a pointer to a function taking a `stStrat *` and returning nothing. The array hoding these function is probably defined as:

```c
stFunction ST_OPERATIONS[] = {
  &stOpFunc1,
  &stOpFunc2,
  ...
};
```

> **Hint**: In the PSX Croc 1 European beta, these pointers are statically stored starting at `0x6AC70`.

The opcode of each instruction is just it's offset into the array. For example, the `PlayAnim` function is the 12th in the array in Croc 1 PSX Demo, so its opcode in this game is `0C`.

#### Processing stratigies in Croc 1 PSX Demo

In order to run a strat (in `stProcessStratigies`), the game will call the next instruction assocaited with the offset in the stream until a flag is set that tells the game it has finished processing the instructions in the strat.

For example:

```c
stStrat *strat;
// ...
while ((strat->flags & ST_FLAG_FINISHED) == 0) {
	(ST_OPERATIONS[stPeekByte(strat)])(strat); // note that instructions in this version are one byte
}
```

Note that the use of 'peek' here implies that the instruction stream's head is not actually pushed forward. This raises an intesting question: how does the instruction stream move along? The answer is that the instructions themselves move the stream forward.

For example, in most instructions will at least be:

```c
void stInstruction(stStrat *strat) {
	strat->instructionStream += 1;
}
```

Processing is basically the same in the final game; there are just a few extra opcodes.

#### Processing strats in Croc 2 PSX Demo

The Croc 2 PSX demo appears to be a bit different. While the game still has a jump table for strats, the finer details seem to be a bit different.

Firstly, opcodes seem to be 32-bit (4 bytes) as compared with the single byte opcodes on Croc 1 demo. Secondly, the while loop seems to increment the program counter for each function as well as do some other variable setting.

### Sources and Resources

* [Croc 2 Strat Function List](https://pastebin.com/Q5aSxcpf) - A list of instructions in Croc 2.
* [Croc 1 PSX Demo Function List](https://github.com/knot126/Stratigise/blob/trunk/doc/Croc1/psx%20demo%20function%20list%20in%20order.txt) - In offset order, so that, for example, stCommandError is actully the 0x00 opcode.
* [Reddit: "Argonaut Strat Language: historical game tool"](https://www.reddit.com/r/gamedev/comments/9xl53d/argonaut_strat_language_historical_game_tool/e9tz6jk/) - Reddit post about being coroutine-based.
* [Croc 2 Beta Playthrough with your Questions and Answers](https://www.youtube.com/watch?v=Ud2UW0B3NNk) - At [23:41](https://youtu.be/Ud2UW0B3NNk?t=1422) he dismisses that it is coroutine-based.
* [Croc Designer Diary](https://web.archive.org/web/20030303184324/http://www.videogames.com/features/universal/croc_dd/index.html) ([Markdown version](https://gist.github.com/knot126/74bdfd189fafa969f651d97488106684)) - Game design for Croc by Nic Cusworth, discusses strats in pages 3 and 4 of last entry
* [Screenshot of first lines of `stEvaluate` in Croc 1](https://cdn.discordapp.com/attachments/347524018334859265/971494443968503878/unknown.png)
* [Stratigise](https://github.com/knot126/Stratigise) - Early WIP dissassembler with some docs about the format
* Own research using PSX EU Demo, Croc DE and Ghidra

## (Croc 2) Registry options

There seems to be an unused or at least unavailable registry option that will disable the fading between levels. Search for `Croc2` in regedit. There are some others, like gamma but I don't think they work.

## (Croc 2) 60 FPS hacks

So far, I have found you can change these values that are related to the update rate of the game:

| Address(es) | Original               | Modified                | Comment |
| ----------- | ---------------------- | ----------------------- | ------- |
| `0x21429`, `0x21465` | `6a 1e` (`push 30`)    | `6a 3c` (`push 60`)     | N/A |

They result in the game running at 60 FPS but updating physics more frequently as well. I am trying to find if the delta time can just be changed for physics things to make it run at "half twice speed", but that is proving quite hard for me so far.

This can also be changed and might be related, but they don't seem to do anything visible:

| Address(es) | Original               | Modified                | Comment |
| ----------- | ---------------------- | ----------------------- | ------- |
| `0x215E7`   | `83 fe 1e`             | `83 fe 3c`              | N/A     |
| `0x215ED`   | `be 1e 00 00 00`       | `be 3c 00 00 00`        | N/A     |
| `0xA5588`   | `00 00 f0 41` (30.0f)  | `00 00 70 42` (60.0f)   | N/A     |

This is an incomplete decompilation of the part of `DoTimers` that is most relivant to changing these constants:

```c
    else {
      QueryPerformanceCounter((LARGE_INTEGER *)&performance);
      temp = hiResTimeSupportedResult;
      performance_ = performance;
      currentTime2_ = currentTime2;
      _preformance_ = performance;
      DAT_004befbc = hiResTimeSupportedResult;
      deltaTimesFixedFramerate =
           __allmul(currentTime2 - currentTime,
                    (timerInitialised - usingHiresTime) - (uint)(currentTime2 < currentTime),0x1e,0)
      ;
      deltaTime = __alldiv(deltaTimesFixedFramerate,performanceFrequency,HighResTimeValue);
      deltaTimesFixedFramerate =
           __allmul(performance_ - currentTime2_,
                    (temp - timerInitialised) - (uint)(performance_ < currentTime2_),0x1e,0);
      i = __alldiv(deltaTimesFixedFramerate,performanceFrequency,HighResTimeValue);
      deltaTime = deltaTime + i;
      frameTime = deltaTime;
      if (!bVar2) {
        bVar2 = true;
        local_10 = performance_ - currentTime;
        iStack12 = (temp - usingHiresTime) - (uint)(performance_ < currentTime);
        i = DAT_004bf060 + 1;
        DAT_004bf060 = i;
        (&timers_0x0)[i] =
             1.0 / ((30.0 / (float)CONCAT44(HighResTimeValue,performanceFrequency)) *
                   (float)CONCAT44(iStack12,local_10));
        if (0x1d < i) {
          DAT_004bf060 = 0;
        }
      }
      currentTime = performance_;
      usingHiresTime = temp;
    }
  } while (deltaTime == 0);
  if (0x1e < deltaTime) {
    deltaTime = 0x1e;
    frameTime = 0x1e;
  }
```

Note that I am only considering the implementation that uses `QueryPerformanceCounter()` since that is gaurnetted to be supported since Windows 7, which is where the 60 FPS mod would be most useful. The game can also use `timeGetTime()` but won't use this if `QueryPerformanceCounter()` is supported.

## Other helpful things

 * [hdc0/Croc-2-mods](https://github.com/hdc0/Croc-2-mods)
 * [OverSurge/PS1-Argonaut-Reverse](https://github.com/OverSurge/PS1-Argonaut-Reverse)
 * [Croc Explorer](https://github.com/zeroKilo/CrocExplorerWV)
 * [Croc 2 Explorer](https://github.com/zeroKilo/Croc2ExplorerWV)
 * [Debug Symbols for C1/C2 on PSX](https://mega.nz/folder/YGAjlICB#YoUGWaXO_KSABy3zjBus7w/folder/VGBlnaJC)
 * [PlayStation Executeable Loader for Ghidra](https://github.com/lab313ru/ghidra_psx_ldr)
 * [Croc 2 PSX Demo symbol import script](https://gist.github.com/knot126/bc2fe3d7663ac1fdb179efd8cb433fe3)
 * [BRender Reference Manual](https://rr2000.cwaboard.co.uk/R4/BRENDER/TEBK_1.HTM)

### Misc.

 * [Ghidra Scripting API](https://ghidra.re/ghidra_docs/api/ghidra/program/flatapi/FlatProgramAPI.html)
 * [Helpful Ghidra API Examples](https://github.com/HackOvert/GhidraSnippets)
 * [Crafting Interpreters](http://craftinginterpreters.com/contents.html)