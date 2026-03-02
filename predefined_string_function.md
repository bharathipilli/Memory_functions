# 📌 String Functions in C (`<string.h>`)

In C, **strings are arrays of characters terminated by a null character `'\0'`.**  
The `<string.h>` library provides many predefined functions for **string manipulation**.

---

# 🔑 Categories of String Functions

1. **Copying & Moving Strings**
   - `strcpy()`
   - `strncpy()`
   - `strdup()` *(non-standard but widely available)*
   - `strcat()`
   - `strncat()`

2. **Comparing Strings**
   - `strcmp()`
   - `strncmp()`
   - `strcasecmp()` *(POSIX extension)*

3. **Searching in Strings**
   - `strchr()`
   - `strrchr()`
   - `strstr()`
   - `strcasestr()` *(POSIX extension)*
   - `strpbrk()`
   - `strcspn()`
   - `strspn()`

4. **Utility Functions**
   - `strlen()`
   - `strtok()`
   - `strerror()`

---

## 1. Copying & Moving Strings

### `strcpy`

```c
char *strcpy(char *dest, const char *src);
````

* Copies string `src` (including `'\0'`) into `dest`.

✅ Example:

```c
char src[] = "Hello";
char dest[20];
strcpy(dest, src);
printf("%s\n", dest);  // Output: Hello
```

---

### `strncpy`

```c
char *strncpy(char *dest, const char *src, size_t n);
```

* Copies up to `n` characters.
* If `src` is shorter, fills remaining with `'\0'`.

✅ Example:

```c
char src[] = "Hi";
char dest[5];
strncpy(dest, src, sizeof(dest));
printf("%s\n", dest);  // Output: Hi
```

---

### `strdup` (non-standard, POSIX)

```c
char *strdup(const char *s);
```

* Allocates new memory and copies string.
* Requires `free()` later.

✅ Example:

```c
char *copy = strdup("OpenAI");
printf("%s\n", copy); // Output: OpenAI
free(copy);
```

---

### `strcat`

```c
char *strcat(char *dest, const char *src);
```

* Appends `src` to `dest`.

✅ Example:

```c
char str[20] = "Hello";
strcat(str, " World");
printf("%s\n", str);  // Output: Hello World
```

---

### `strncat`

```c
char *strncat(char *dest, const char *src, size_t n);
```

* Appends up to `n` characters.

✅ Example:

```c
char str[20] = "Good";
strncat(str, " Morning", 4);
printf("%s\n", str);  // Output: Good Mor
```

---

## 2. Comparing Strings

### `strcmp`

```c
int strcmp(const char *s1, const char *s2);
```

* Returns:

  * `0` if equal
  * `<0` if `s1 < s2`
  * `>0` if `s1 > s2`

✅ Example:

```c
printf("%d\n", strcmp("abc", "abc")); // 0
printf("%d\n", strcmp("abc", "abd")); // -1
```

---

### `strncmp`

```c
int strncmp(const char *s1, const char *s2, size_t n);
```

* Compares first `n` characters.

✅ Example:

```c
printf("%d\n", strncmp("hello", "helium", 3)); // 0
```

---

### `strcasecmp` (POSIX)

```c
int strcasecmp(const char *s1, const char *s2);
```

* Case-insensitive comparison.

✅ Example:

```c
printf("%d\n", strcasecmp("HELLO", "hello")); // 0
```

---

## 3. Searching in Strings

### `strchr`

```c
char *strchr(const char *str, int c);
```

* Finds first occurrence of character.

✅ Example:

```c
char *p = strchr("abcdef", 'c');
printf("%s\n", p);  // Output: cdef
```

---

### `strrchr`

```c
char *strrchr(const char *str, int c);
```

* Finds last occurrence.

✅ Example:

```c
char *p = strrchr("banana", 'a');
printf("%s\n", p);  // Output: a
```

---

### `strstr`

```c
char *strstr(const char *haystack, const char *needle);
```

* Finds first occurrence of substring.

✅ Example:

```c
char *p = strstr("hello world", "world");
printf("%s\n", p);  // Output: world
```

---

### `strcasestr` (POSIX)

```c
char *strcasestr(const char *haystack, const char *needle);
```

* Case-insensitive substring search.

✅ Example:

```c
char *p = strcasestr("Hello World", "world");
printf("%s\n", p);  // Output: World
```

---

### `strpbrk`

```c
char *strpbrk(const char *str1, const char *str2);
```

* Finds first character from `str2` in `str1`.

✅ Example:

```c
char *p = strpbrk("abcdef", "xzcd");
printf("%s\n", p);  // Output: cdef
```

---

### `strcspn`

```c
size_t strcspn(const char *str1, const char *str2);
```

* Length of initial segment not containing any from `str2`.

✅ Example:

```c
printf("%zu\n", strcspn("abcdef", "de")); // 3
```

---

### `strspn`

```c
size_t strspn(const char *str1, const char *str2);
```

* Length of initial segment containing only from `str2`.

✅ Example:

```c
printf("%zu\n", strspn("abcdef", "abc")); // 3
```

---

## 4. Utility Functions

### `strlen`

```c
size_t strlen(const char *str);
```

* Returns length (excluding `'\0'`).

✅ Example:

```c
printf("%zu\n", strlen("OpenAI")); // 6
```

---

### `strtok`

```c
char *strtok(char *str, const char *delim);
```

* Splits string into tokens.
* ⚠️ Modifies original string.

✅ Example:

```c
char str[] = "one,two,three";
char *token = strtok(str, ",");
while (token) {
    printf("%s\n", token);
    token = strtok(NULL, ",");
}
```

---

### `strerror`

```c
char *strerror(int errnum);
```

* Returns human-readable error string.

✅ Example:

```c
#include <errno.h>
printf("%s\n", strerror(2)); // Output: No such file or directory
```

---

# 📊 Summary Table

| Function     | Purpose                    |
| ------------ | -------------------------- |
| `strcpy`     | Copy string                |
| `strncpy`    | Copy with limit            |
| `strdup`     | Duplicate string (heap)    |
| `strcat`     | Concatenate strings        |
| `strncat`    | Concatenate with limit     |
| `strcmp`     | Compare strings            |
| `strncmp`    | Compare with limit         |
| `strcasecmp` | Case-insensitive compare   |
| `strchr`     | Find first char            |
| `strrchr`    | Find last char             |
| `strstr`     | Find substring             |
| `strcasestr` | Case-insensitive substring |
| `strpbrk`    | Find any char from set     |
| `strcspn`    | Span without chars         |
| `strspn`     | Span with chars            |
| `strlen`     | String length              |
| `strtok`     | Tokenize string            |
| `strerror`   | Error message              |

---

# 🚀 Notes

* Always allocate enough memory for destination buffers when using `strcpy`/`strcat`.
* Use safer alternatives like `strncpy` to prevent **buffer overflows**.
* Some functions (`strdup`, `strcasecmp`, `strcasestr`) are **POSIX extensions**, not part of ISO C standard.

```
---

👉 Do you also want me to combine **Memory Functions + String Functions** into **one complete `.md` handbook** (like a ready interview/reference guide)?
```
