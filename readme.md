# ruby-build definition for ree-1.8.7-2012.02 using glibc 2.18 (w/ GCC 4.8)

This build definition allows for easily compiling ree-1.8.7-2012.02 on Linux distros that use glibc 2.18, such as Arch Linux.

Usually, ruby-build is run via rbenv, so the instructions below use `rbenv` for the installation.

```shell
git clone git://github.com/veracross/ruby-build-ree-1.8.7-2012.02-glibc-2.18.git
cd ruby-build-ree-1.8.7-2012.02-glibc-2.18
rbenv install ./ruby-build-ree-1.8.7-2012.02
```

## Why

This build definition patches the google-perftools-1.7 package to work with glibc 2.18.

```
src/tcmalloc.cc: At global scope:
src/tcmalloc.cc:1672:54: error: conflicting declaration ‘void* (* __memalign_hook)(size_t, size_t, const void*)’
 void *(*__memalign_hook)(size_t, size_t, const void *) = MemalignOverride;
                                                      ^
In file included from src/tcmalloc.cc:101:0:
/usr/include/malloc.h:160:39: error: ‘__memalign_hook’ has a previous declaration as ‘void* (* volatile __memalign_hook)(size_t, size_t, const void*)’
 extern void *(*__MALLOC_HOOK_VOLATILE __memalign_hook) (size_t __alignment,
                                       ^
Makefile:3317: recipe for target 'libtcmalloc_minimal_la-tcmalloc.lo' failed
make: *** [libtcmalloc_minimal_la-tcmalloc.lo] Error 1
```
