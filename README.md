# rhash_md5.c

This is an [MD5](https://en.wikipedia.org/wiki/MD5) implementation from Aleksey Kravchenko's [RHash utility](http://rhash.anz.ru/), extracted for use with the [clib package manager](https://github.com/clibs/clib).

## Installation

Install with [clib](https://github.com/clibs/clib):

```
$ clib install pepaslabs/rhash_md5.c
```

## API

```c
void rhash_md5_init(md5_ctx *ctx);
void rhash_md5_update(md5_ctx *ctx, const unsigned char* msg, size_t size);
void rhash_md5_final(md5_ctx *ctx, unsigned char result[16]);
```

## Usage

Dump this into a console to build a test program:

```
cd /tmp
cat > main.c << 'EOF'
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>

#include "rhash_md5/md5.h"

int main(int argc, char **argv) {
    // compute the MD5 sum of the string "Hello, World!"
    md5_ctx ctx;
    unsigned char hash[16];
    rhash_md5_init(&ctx);
    rhash_md5_update(&ctx, (const unsigned char *)"Hello, World!", 13);
    rhash_md5_final(&ctx, hash);

    // print the (binary) MD5 sum to stdout
    write(fileno(stdout), hash, 16);

    return EXIT_SUCCESS;
}
EOF
clib install pepaslabs/rhash_md5.c
gcc -Wall -Werror -c deps/rhash_md5/*.c
gcc -Wall -Werror -Ideps *.o main.c
```

Try it out!

```
$ ./a.out | hexdump
0000000 65 a8 e2 7d 88 79 28 38 31 b6 64 bd 8b 7f 0a d4
0000010
```

Verify the output against your system's `md5` utility.

On a mac:

```
$ echo -n 'Hello, World!' | md5
65a8e27d8879283831b664bd8b7f0ad4
```

On linux:

```
$ echo -n 'Hello, World!' | md5sum
65a8e27d8879283831b664bd8b7f0ad4  -
```

## License

Quoting from http://rhash.anz.ru/license.php (as of 2016/11/1):

> License

> The RHash program and LibRHash library are  distributed under  RHash License,
(see below). Basically, the program, library and source code can be used free
of charge in Open Source, Commercial and other projects. In the case an  OSI-
approved license is required the  MIT license should be used.

In accordance with the above, I am redistributing this code under the terms of the [MIT license](https://opensource.org/licenses/MIT).
