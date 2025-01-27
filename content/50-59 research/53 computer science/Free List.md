A set of elements that describes the free space available for use in OS memory.

It's a linked list that as follows:
```mermaid
graph LR;
A[head] --> B[addr:0 \n size: 4]
B --> C[addr:10 \n size: 2]
C --> D[NULL]
```

In order to track the size of allocated regions, most allocators store metadata in a header block (e.g. size, magic number for integrity checking etc). It's considered as overhead, just before allocated unit. 
- `free(void *ptr)` does not take a size parameter since ..

For example, assume a header where
```c
typedef struct {
	int size;
	int magic;
} header_t;
```

If the user requests 20 bytes,
```c
ptr = malloc(20)
```

then, in the OS:
```c
void free(void *ptr) {
	header_t *hptr = (header_t *) ptr - 1; // why 1?
	total_size_to_free = hptr->size + sizeof(hptr)
}
```

Where is the free list stored? Inside the free space built as:
`node_t = malloc(sizeof(node_t))` where node type is
```c
typedef struct __node_t {
	int size;
	struct __node_t *next;
} node_t;
```

But we are trying to make malloc! So, assume it takes 4KB free space to manage:
```c
// free space acquired via system call mmap()
node_t *head = mmap(NULL, 4096, ...)
// init the heap and puts the first element of the free list inside that space
head->size = 4096 - sizeof(node_t)
head->next = NULL;
```

If the user request 100 bytes, let's assume 8 byte header. Then, we need to find a free list node big enough for "108" bytes. If we are running out of free space, ask OS to allocate for more.

**Splitting**
The smaller a block is, the less likely it is to be used. Any request > 4 will fail, but what about < 4 e.g. 1.

Option 1:
```mermaid
graph LR;
A[head] --> B[addr:1 \n size: 3]
B --> C[addr:10 \n size: 2]
C --> D[NULL]
```

Option 2:
```mermaid
graph LR;
A[head] --> B[addr:1 \n size: 3]
B --> C[addr:11 \n size: 1]
C --> D[NULL]
```

**Coalescing**
What happens if we free(4) i.e. free 4 bytes of data?
Option 1: Simply free that unit and add it to free list.
```mermaid
graph LR;
A[head] --> B[addr:0 \n size: 4]
B --> C[addr:4 \n size: 6]
C --> D[addr:10 \n size: 2]
D --> E[NULL]
```

Option 2: Free and merge free neighbouring units to 1 (Coalescing)
```mermaid
graph LR;
A[head] --> B[addr:0 \n size: 12]
B --> D[NULL]
```

Better version: [[Segregated Free Lists]]