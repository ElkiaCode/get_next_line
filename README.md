# get_next_line

*Read a file descriptor one line at a time. A 42 curriculum project in C.*

`get_next_line(fd)` returns the next line from `fd`, including the trailing `\n` when there is one. It returns `NULL` at end of file or on error. Between calls, a `static` buffer keeps the bytes that were read but not yet returned, so each call reads only as much as it needs.

## Usage

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int   fd = open("file.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
}
```

Compile with a buffer size of your choice:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c main.c
```

## Files

- `get_next_line.c`: reads, stores leftover bytes and extracts the line
- `get_next_line_utils.c`: string helpers (`strlen`, `strjoin`, `strchr`…)
- `get_next_line.h`

## Author

[ElkiaCode](https://github.com/ElkiaCode) (cparodi), 42 Nice.
