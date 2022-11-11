```c
#include <string.h>
void* memcpy (void* dest, const void* source, size_t num)
```

**첫번째 인자 void* dest**= **복사 받을** 메모리를 가리키는 포인터

**두번째 인자 const void* source**= **복사할** 메모리를 가리키고 있는 포인터

**세번째 인자 size_t num**= 복사할 데이터(값)의 길이(바이트 단위)