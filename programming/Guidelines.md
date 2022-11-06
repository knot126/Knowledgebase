# General programming guidelines

Some intresting programming guidelines, some of which are strange. They aren't always followed, and for good reason. They are not rules!

## Do repeat yourself (in comments)!

*But be smart about it!*

This is probably an odd one since you have probably been told "don't repeat yourself."

In pure code, yes, you should try condense things and put everything into functions or `using` blocks after you have written something more than three times or so.

However, there are advantages to describing every few lines of code in a comment, or describing how a function works in some level of detail.

### Advantages

Consider that:

* Writing comments frequently means that you effectively wrote it twice: one in a very formal way, and one in a very informal way.
* This duality makes the code or comment easier to understand since you can always fall back on one or the other.
* Using this, you can also make sure you understand what every part of your code is doing since you have effectively reviewed it.
* And you can easily demonstrate knowledge (or lack thereof) concerning what you have written, including any flaws in understanding that might not be obvious from source.
* It can help you spot errors by recogising when the comment and code don't match!

### Disadvantages

But also keep in mind that:

* It's a lot more work to write comments and code at the same time.
* You are repating yourself, and you can make mistakes that just make everything more confusing. Especially so when code and comments don't align.
* It's not a free ticket to write bad code just becuase someone could fix it later based on your description.
* It's not a free ticket to write overly complex code just because you can explain it very well.
* It can be tring if you've written something a thousand times.

### So, what?

Ultimately, you should "over-comment" your code if it makes sense to do so. Nither is "correct."

## Naming

I really don't care about naming schemes. I like `PascalCase` or `snake_case` or even `Whatever_This_Is` and even `kebab-case`.

However, I only think `camelCase` works sometimes, like in method names for objects. It can feel quite unbalanced which can make code hard to read.

Generally, I pick one of these for large projects, but also long as it is consistent it is fine:

<details>
<summary>Melon-style</summary>

```c
typedef struct XxVector3 {
	float x, y, z;
} XxVector3;

typedef enum XxLogLevel {
	XX_LOG_LEVEL_INFO = 0,
	XX_LOG_LEVEL_ERROR = 1,
} XxLogLevel;

void XxLog(LogLevel level, const char * restrict message);

XxVector3 XxVector3Add(Vector3 left_vector, Vector3 right_vector) {
	XxVector3 new_vector;
	
	new_vector.x = left_vector.x + right_vector.x;
	new_vector.y = left_vector.y + right_vector.y;
	new_vector.z = left_vector.z + right_vector.z;
	
	return new_vector;
}

int main(void) {
	XxLog(XX_LOG_LEVEL_INFO, "Hello, world!");
	return 0;
}
```
</details>

<details>
<summary>Nectarine-style</summary>

```c
typedef struct XX_Vector3 {
	float x, y, z;
} XX_Vector3;

typedef enum XX_Log_Level {
	XX_LOG_LEVEL_INFO = 0,
	XX_LOG_LEVEL_ERROR = 1,
} XX_Log_Level;

void XX_Log(Log_Level level, const char * restrict message);

XX_Vector3 XX_Vector3_Add(Vector3 left_vector, Vector3 right_vector) {
	Vector3 new_vector;
	
	new_vector.x = left_vector.x + right_vector.x;
	new_vector.y = left_vector.y + right_vector.y;
	new_vector.z = left_vector.z + right_vector.z;
	
	return new_vector;
}

int main(void) {
	XX_Log(XX_LOG_LEVEL_INFO, "Hello, world!");
	return 0;
}
```
</details>