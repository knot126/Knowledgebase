# Quick Run

**Quick Run** was supposed to be an endless runner without the quickstep or "lanes" typically seen in mobile endless runners, in addition to speed control options. It would essentially have been like *Crash on the Run* or *Temple Run*, but different enough to provide room to distinguish it from other games like it.

The initial version of the "engine" from 2019 was going to be written in Python, with a plan for a 2.0 C++ engine rewrite in the future. That didn't go very far as writing this engine was my first time writing code *ever* (aside from a C++ hello world), so it turned out being some crappy code that just printed lots of things but never really acted like a game.

For most of 2020, I worked on modding prexisting video games. Nothing really happened at the time as I worked quite a lot with my attempts to write tools for those games. I tried to start one or two sample applications in Vulkan, but I found the API to be overly verbose.

At the very start of the new year, I had built a prototype of the game I would want to make in Unity (and later a slightly better one in Godot) and decided that if I could do it well, the game was worth making. I started to write an engine in C++, making a few basic 3D vector classes but not really going anywhere.

A few months in to 2021, I cleaned slate and started building a game enigne in C as I hadn't really been enjoying C++ for practial purposes. The engine didn't initially have a name (the folder was just called `Engine`) and for it's first few months was OpenGL and GLEW spegetti code. First it just drew the "Hello Graphics" RGB triangle, then I was able to draw a textured rectangle, then a rotating mess of stuff, then a cube, then many cubes and so on... I was following a site called LearnOpenGL, so I had things working in roughly that lineage.

As part of these tests, I also began to develop my own core utilities library written from scratch, which contained things like time tools, file reading and writing, XML loading and even a custom memory allocator, which would be seprate from the engine. This was a very good idea as parts of the initial core utilities still live on as Melon, even after the discontinuation of the original Quick Run Engine.

After a while, I started drawing more interactive things, such as a rotating cube with a camera that slowly moved along. Though, I think my engine became a "real" game engine when I added Lua scripting support.

The initial scripting API looked a lot like Smash Hit's, even using the same `mg` prefix for function names and essentially one-for-one copying the naming scheme for UI functions. The engine had also become based on a fairly pure Entity-Component-System architecture, which do various things to make the best use of CPU cache.

Here are a few small pieces of some original scripts:

```lua
function initHud()
	ui.Statistics = mgUIElement(QR_ELEMUI_TEXT)
	mgUIText(ui.Statistics, "[text about in-game statistics will appear here shortly...]")
	mgUITextPos(ui.Statistics, -1.0, -0.9)
	mgUITextSize(ui.Statistics, 0.1)
	mgUITextColour(ui.Statistics, 0.0, 1.0, 0.3, 1.0)
	
	ui.LivesCountText = mgUIElement(QR_ELEMUI_TEXT)
	mgUIText(ui.LivesCountText, "Lives")
	mgUITextPos(ui.LivesCountText, -0.95, 0.95)
	mgUITextSize(ui.LivesCountText, 0.06)
	-- There was more here..
end
```

* `ui` was a table in Lua.

```lua
function init()
	-- player init
	local player = new_cube(0.0, 1.5, 0.0, 0.9, 0.9, 0.9, true, QR_PHYS_ENABLE_RESPONSE, "assets://mesh/player.obj")
	mgActivePlayer(player)
	
	lives.count = 5
	lives.updated = true
	
	initHud()
	
	first = mgEntity(0)
end
```

 * `new_cube` isn't a provided function, instead, there was an `include.lua` script that was included in every other script which defined functions like it:

```lua
function new_cube(x, y, z, sx, sy, sz, phys, pflags, model)
	local flags = QR_COMPONENT_TRANSFORM | QR_COMPONENT_MESH
	if phys then
		flags = flags | QR_COMPONENT_PHYSICS
	end
	local ent = mgEntity(flags)
	
	mgTransform(ent, x, y, z, 0.0, 0.0, 0.0, sx, sy, sz)
	mgMesh2(ent, model)
	if phys then
		mgMass(ent, 1.0)
		mgForce(ent, 0.0, 0.0, -100.0, 0.0, 0.0, 0.0)
		if pflags ~= nil then
			mgPhysFlags(ent, pflags)
		end
	end
	
	return ent
end
```

As you can see from the scripts, I also added a very basic physics system based on AABBs and using euler integration. While I had intended to write a more complete physics system with full 3D mesh support, I never got that far.

Eventually, I started to write some other systems. There was a basic bitmap (pre-rendered) font system. You could draw UI rectangles to create basic HUDs. And at some point you could load basic Wavefront OBJ format models.

After a bit more time, I decided that just copying the Smash Hit Lua API wasn't the best thing to do, and I decided to rewrite the scripting interface so that it moved to `snake_case` names and refactor the Entity-Component-System so that the components and the systems were now assocaited together, making some operations more nicely organised but making subsystem interoperability a bit more complex.

After the rewrite, my scripts started to look more like this:

```lua
function init()
	-- Create camera
	cam = create_entity(ENT_TRANSFORM)
	push_transform(cam, 0.0, 5.0, 5.65, 0.0375, 0.0, 0.0)
	set_camera(cam)
	
	-- Initialise player
	player = make_box(0.0, 2.0, -2.0)
	set_physics_flags(player, PHYSICS_MODE_PLAYER)
	
	-- Sync the physics graph after everything has been created
	physics_sync_graph()
	
	-- Set some registry values
	reg_set("life", "3")
	reg_set("offset", "5230")
	
	-- Try making a rectangle
	R = make_rect(0.0, 0.875, 2.0, 0.25, 0.0, 0.0, 0.0, 0.4)
	
	-- Open the level script
	level = script_open("assets://levels/test.lua")
	
	-- Enable the physics engine
	enable_physics(true)
	
	-- Disable mouse cursor (for camera)
	set_mouse_disabled(true)
end
```

I actually think that from a user's perspective, it was a decent engine at this point. Of course, good news does not last forever, and from my perspective as the engine developer things were pretty bad...

After a quick tangent into working with Bezier surfaces, I really started to look at my engine. There were a lot of little bugs and issues. Maybe those could be fixed. But of course, my lack of understanding what I was doing with OpenGL and the graphics and physics side of my engine wasn't something that was easily fixed, and with increasing ambition about what I would like the engine to be able to do, things fell apart quickly as I lost intrest in building the game and its engine due to both dissatisfactions with the engine itself and unrelated personal issues that came at the worst possible time.

Ultimately, I found that I really didn't have the knowledge I needed to build a mono-game engine for my game, let alone a mutli-game engine, and I certainly wasn't adept enough to do more advanced ("advanced" being relative to me at the time) things like bezier surfaces handling or triangle collision detection that would have at least made the game start to feel comlpete.

But of course, I did learn a lot. First, I learnt that I really need to understand what I'm doing in order to feel confident in the code that I am writing. I need to understand how and why something works, and the theory behind it.

Just getting the result on screen seems more important at first. And occasinally for small scripts you will never touch again, it can be okay to say that. But if you are making a big system you should really understand every part that you are responsible for (and generally as many as you can possibily know about) so that you don't make a mess (or more accurately: so that you make a manageable mess that you can navigate).

Second, I learnt that hyperfocusing on one design pattern isn't really a good idea. I might not have explicitly stated it, but I focused on Entity-Component-Systems and cache efficecy way too much. Sure, it's good to write fast code if you can, and ECS can speed up games in cases, but it was pointed out to me that an ECS only works if you loop over entities frequently. The fun thing is: you don't nessicairally have to do that so often that an ECS will really help you; or, rather, there is enough computing power even in mobile chips from 2010 that it doesn't matter much. Had I not insisted on a "cache friendly" design (which I didn't even test), maybe the engine would have been a lot nicer to maintain and even to use.

Thirdly, I learnt things about what I like to do: game development is stressful without having the overhead of a team and the problems related to crunch (among other things). This exprience has at least made me think harder about the kind of place I would like to work. While I have not eliminated gamedev as something I could do, this exprience combined with knowledge about issues in gamedev has at least in part lead me to call my new engine project, Trestle, a real time simulations and games engine instead of primarily a game engine.

There are probably more things I took away from this. For one, I like simple, easy to use but hard to master programming languages over complex though "easy" to use ones. But that's getting a bit long.

The biggest takeaway is that, yes, I failed to make a game and it's engine, but I did learn a lot. I think I've done everything I should with this failure - that is, to learn from it - and I can safely and cleanly pepare for what comes next. Trestle is going to be my largest project ever - and I'm going to make sure I prepare for it well, and stop myself when I need to prepare more. □
