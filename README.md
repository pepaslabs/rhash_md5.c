# rhash_md5.c

This is an [MD5](https://en.wikipedia.org/wiki/MD5) implementation from Aleksey Kravchenko's [RHash utility](http://rhash.anz.ru/), extracted for use with the [clib package manager](https://github.com/clibs/clib).

## Installation

Install with [clib](https://github.com/clibs/clib):

```
$ clib install pepaslabs/rhash_md5.c
```

## API

```
void rhash_md5_init(md5_ctx *ctx);
void rhash_md5_update(md5_ctx *ctx, const unsigned char* msg, size_t size);
void rhash_md5_final(md5_ctx *ctx, unsigned char result[16]);
```

## License

Quoting from http://rhash.anz.ru/license.php (as of 2016/11/1):

> License

> The RHash program and LibRHash library are  distributed under  RHash License,
(see below). Basically, the program, library and source code can be used free
of charge in Open Source, Commercial and other projects. In the case an  OSI-
approved license is required the  MIT license should be used.

In accordance with the above, I am redistributing this code under the terms of the [MIT license](https://opensource.org/licenses/MIT).
