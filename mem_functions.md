# 📌 Memory Functions in C (`<string.h>`)

In C, **memory functions** are provided in the `<string.h>` library to manipulate raw memory blocks (not null-terminated strings).  
They work with arbitrary data (bytes), not necessarily characters.

There are **5 main memory functions**:

---

## 1. `memset`

```c
void *memset(void *ptr, int value, size_t num);
````

### 📖 Description

* Sets the first `num` bytes of the memory block pointed to by `ptr` with the given `value`.
* `value` is converted to an **unsigned char** and stored in memory.

### ✅ Example

```c
#include <stdio.h>
#include <string.h>

int main() {
    char arr[10];
    memset(arr, 'A', sizeof(arr));

    for (int i = 0; i < 10; i++) {
        printf("%c ", arr[i]);  // Output: A A A A A A A A A A
    }
    return 0;
}
```

---

## 2. `memcpy`

```c
void *memcpy(void *dest, const void *src, size_t num);
```

### 📖 Description

* Copies `num` bytes from memory area `src` to memory area `dest`.
* ⚠️ **Does not handle overlapping regions**. Behavior is undefined if overlap occurs.
* Faster than `memmove`.

### ✅ Example

```c
#include <stdio.h>
#include <string.h>

int main() {
    char src[] = "Hello";
    char dest[10];

    memcpy(dest, src, strlen(src) + 1); // +1 for '\0'

    printf("Copied String: %s\n", dest);  // Output: Hello
    return 0;
}
```

---

## 3. `memmove`

```c
void *memmove(void *dest, const void *src, size_t num);
```

### 📖 Description

* Copies `num` bytes from `src` to `dest`.
* ✅ Safe for overlapping regions (unlike `memcpy`).
* Internally, it checks overlap and decides whether to copy **forwards or backwards**.

### ✅ Example

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[20] = "1234567890";

    // Overlapping copy
    memmove(str + 4, str, 6);

    printf("Result: %s\n", str); // Output: 1234123456
    return 0;
}
```

---

## 4. `memcmp`

```c
int memcmp(const void *ptr1, const void *ptr2, size_t num);
```

### 📖 Description

* Compares the first `num` bytes of two memory blocks.
* Returns:

  * `0` if equal
  * `<0` if `ptr1 < ptr2`
  * `>0` if `ptr1 > ptr2`

### ✅ Example

```c
#include <stdio.h>
#include <string.h>

int main() {
    char a[] = {1, 2, 3};
    char b[] = {1, 2, 4};

    int res = memcmp(a, b, 3);
    if (res == 0) printf("Equal\n");
    else if (res < 0) printf("a < b\n"); // Output: a < b
    else printf("a > b\n");
    return 0;
}
```

---

## 5. `memchr`

```c
void *memchr(const void *ptr, int value, size_t num);
```

### 📖 Description

* Searches the first `num` bytes of the block pointed to by `ptr` for the first occurrence of `value` (converted to unsigned char).
* Returns:

  * Pointer to the first match
  * `NULL` if not found

### ✅ Example

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "abcdef";

    char *pos = memchr(str, 'd', strlen(str));
    if (pos != NULL)
        printf("Found 'd' at position: %ld\n", pos - str); // Output: 3
    else
        printf("Not found\n");

    return 0;
}
```

---

# 🔑 Summary Table

| Function  | Purpose                  | Overlap Safe | Example Use                 |
| --------- | ------------------------ | ------------ | --------------------------- |
| `memset`  | Fill memory with a value | N/A          | Initialize buffer           |
| `memcpy`  | Copy memory (fast)       | ❌            | Copy arrays                 |
| `memmove` | Copy memory safely       | ✅            | Overlapping copy            |
| `memcmp`  | Compare memory blocks    | N/A          | Sorting/binary data compare |
| `memchr`  | Search in memory         | N/A          | Find byte in buffer         |

---

# 🚀 Notes

* These functions **work with raw bytes**, not necessarily characters or strings.
* Always ensure **allocated memory** is large enough before using them.
* For **strings**, you usually use string functions (`strcpy`, `strlen`, etc.), but for **binary/raw data**, you use these memory functions.

```

---

Do you want me to also create a **separate `.md` file** for all **String Functions in C** (like `strcpy`, `strcat`, `strlen`), just like this?
```
