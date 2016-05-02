---
layout: post
title:  "GitHub Pages導入: DebianにRuby 2.x.xを導入してローカル環境作成"
date:   2016-04-26 09:00:00 +0900
categories: github-pages install
---

これはJekyllというよりRubyのハナシで単にRubyを使っていないから必要になるトピックかもしれないが、ここは今後のためにもいろいろ見ながらということで。

そもそもなんでDebian/Ubuntuのデフォルトのapt-getで古いRubyしかインストールされないのかというのが気になるが。

Rubyサイトの「[Rubyのインストール](https://www.ruby-lang.org/ja/documentation/installation/)」によれば、

>Ruby コミュニティの中の一部のメンバーは Ruby をインストールするのに、 パッケージマネージャを使わず、代わりに専用のツールを使うべきであると強く考えています。 その利点・欠点を詳述するのはこのページの範囲から逸脱するため割愛しますが、 最大の理由は大半のパッケージマネージャは公式リポジトリに古いバージョンの Ruby しかないからです。 もしあなたが新しい Ruby を使いたければ、パッケージ名が正しいか確認するか、 上述した専用ツールを使ってください。

さらに、

>しかしながら、サードパーティ製ツールかパッケージマネージャを使う方が良い考えです。 何故なら、ソースからインストールされた Ruby はどのツールからも管理されないからです。

とあるのだが、ここは取りあえずということでソースからインストールしてしまう。
Jekyll以外でRubyとつきあことがあれば考えよう、それもlearning by doingで。

````````````````````````

$ ./configure --with-openssl-dir=/usr/local/openssl --enable-shared
checking for ruby... /usr/local/bin/ruby
*** using http instead of https ***					← 気になる
config.guess already exists
*** using http instead of https ***
config.sub already exists
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for gcc... gcc

````````````````````````

と延々ときて、

<!--

checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking whether gcc needs -traditional... no
checking for ld... ld
checking whether the linker is GNU ld... yes
checking whether gcc -E accepts -o... yes
checking for ranlib... ranlib
checking for ar... ar
checking for as... as
checking for objdump... objdump
checking for objcopy... objcopy
checking for nm... nm
checking whether ln -s works... yes
checking whether make sets $(MAKE)... yes
checking for a BSD-compatible install... /usr/bin/install -c
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for dtrace... no
checking for dot... no
checking for doxygen... no
checking for pkg-config... pkg-config
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking minix/config.h usability... no
checking minix/config.h presence... no
checking for minix/config.h... no
checking whether it is safe to define __EXTENSIONS__... yes
checking for cd using physical directory... cd -P
checking whether CFLAGS is valid... yes
checking whether LDFLAGS is valid... yes
checking whether -Wno-unused-parameter is accepted as CFLAGS... yes
checking whether -Wno-parentheses is accepted as CFLAGS... yes
checking whether -Wno-long-long is accepted as CFLAGS... yes
checking whether -Wno-missing-field-initializers is accepted as CFLAGS... yes
checking whether -Wunused-variable is accepted as CFLAGS... yes
checking whether -Wpointer-arith is accepted as CFLAGS... yes
checking whether -Wwrite-strings is accepted as CFLAGS... yes
checking whether -Wdeclaration-after-statement is accepted as CFLAGS... yes
checking whether -Wshorten-64-to-32 is accepted as CFLAGS... no
checking whether -Wimplicit-function-declaration is accepted as CFLAGS... yes
checking whether -Wdivision-by-zero is accepted as CFLAGS... no
checking whether -Wdeprecated-declarations is accepted as CFLAGS... yes
checking whether -Wno-packed-bitfield-compat is accepted as CFLAGS... yes
checking whether -Wextra-tokens is accepted as CFLAGS... no
checking whether -Wall -Wextra is accepted as CFLAGS... yes
checking whether -Qunused-arguments is accepted as CFLAGS... no
checking whether INFINITY is available without C99 option... yes
checking whether NAN is available without C99 option... yes
checking whether -D_FORTIFY_SOURCE=2 is accepted as CFLAGS... yes
checking whether -fstack-protector is accepted as CFLAGS... yes
checking whether -fstack-protector is accepted as LDFLAGS... yes
checking whether -std=iso9899:1999 is accepted as CFLAGS... yes
checking whether -fno-strict-overflow is accepted as CFLAGS... yes
checking whether -ggdb3 is accepted as CFLAGS... yes
checking whether -fvisibility=hidden is accepted as CFLAGS... yes
checking whether -fno-fast-math is accepted as CFLAGS... yes
checking for crypt in -lcrypt... yes
checking for dlopen in -ldl... yes
checking for shl_load in -ldld... no
checking for shutdown in -lsocket... no
checking for dirent.h that defines DIR... yes
checking for library containing opendir... none required
checking for stdbool.h that conforms to C99... yes
checking for _Bool... yes
checking for sys/wait.h that is POSIX.1 compatible... yes
checking a.out.h usability... yes
checking a.out.h presence... yes
checking for a.out.h... yes
checking atomic.h usability... no
checking atomic.h presence... no
checking for atomic.h... no
checking direct.h usability... no
checking direct.h presence... no
checking for direct.h... no
checking grp.h usability... yes
checking grp.h presence... yes
checking for grp.h... yes
checking fcntl.h usability... yes
checking fcntl.h presence... yes
checking for fcntl.h... yes
checking float.h usability... yes
checking float.h presence... yes
checking for float.h... yes
checking ieeefp.h usability... no
checking ieeefp.h presence... no
checking for ieeefp.h... no
checking intrinsics.h usability... no
checking intrinsics.h presence... no
checking for intrinsics.h... no
checking langinfo.h usability... yes
checking langinfo.h presence... yes
checking for langinfo.h... yes
checking limits.h usability... yes
checking limits.h presence... yes
checking for limits.h... yes
checking locale.h usability... yes
checking locale.h presence... yes
checking for locale.h... yes
checking malloc.h usability... yes
checking malloc.h presence... yes
checking for malloc.h... yes
checking malloc/malloc.h usability... no
checking malloc/malloc.h presence... no
checking for malloc/malloc.h... no
checking malloc_np.h usability... no
checking malloc_np.h presence... no
checking for malloc_np.h... no
checking net/socket.h usability... no
checking net/socket.h presence... no
checking for net/socket.h... no
checking process.h usability... no
checking process.h presence... no
checking for process.h... no
checking pwd.h usability... yes
checking pwd.h presence... yes
checking for pwd.h... yes
checking setjmpex.h usability... no
checking setjmpex.h presence... no
checking for setjmpex.h... no
checking sys/attr.h usability... no
checking sys/attr.h presence... no
checking for sys/attr.h... no
checking sys/fcntl.h usability... yes
checking sys/fcntl.h presence... yes
checking for sys/fcntl.h... yes
checking sys/file.h usability... yes
checking sys/file.h presence... yes
checking for sys/file.h... yes
checking sys/id.h usability... no
checking sys/id.h presence... no
checking for sys/id.h... no
checking sys/ioctl.h usability... yes
checking sys/ioctl.h presence... yes
checking for sys/ioctl.h... yes
checking sys/mkdev.h usability... no
checking sys/mkdev.h presence... no
checking for sys/mkdev.h... no
checking sys/param.h usability... yes
checking sys/param.h presence... yes
checking for sys/param.h... yes
checking sys/prctl.h usability... yes
checking sys/prctl.h presence... yes
checking for sys/prctl.h... yes
checking sys/resource.h usability... yes
checking sys/resource.h presence... yes
checking for sys/resource.h... yes
checking sys/select.h usability... yes
checking sys/select.h presence... yes
checking for sys/select.h... yes
checking sys/sendfile.h usability... yes
checking sys/sendfile.h presence... yes
checking for sys/sendfile.h... yes
checking sys/socket.h usability... yes
checking sys/socket.h presence... yes
checking for sys/socket.h... yes
checking sys/syscall.h usability... yes
checking sys/syscall.h presence... yes
checking for sys/syscall.h... yes
checking sys/time.h usability... yes
checking sys/time.h presence... yes
checking for sys/time.h... yes
checking sys/times.h usability... yes
checking sys/times.h presence... yes
checking for sys/times.h... yes
checking sys/uio.h usability... yes
checking sys/uio.h presence... yes
checking for sys/uio.h... yes
checking sys/utime.h usability... no
checking sys/utime.h presence... no
checking for sys/utime.h... no
checking syscall.h usability... yes
checking syscall.h presence... yes
checking for syscall.h... yes
checking time.h usability... yes
checking time.h presence... yes
checking for time.h... yes
checking ucontext.h usability... yes
checking ucontext.h presence... yes
checking for ucontext.h... yes
checking utime.h usability... yes
checking utime.h presence... yes
checking for utime.h... yes
checking gmp.h usability... no
checking gmp.h presence... no
checking for gmp.h... no
checking for special C compiler options needed for large files... no
checking for _FILE_OFFSET_BITS value needed for large files... no
checking whether byte ordering is bigendian... no
checking for an ANSI C-conforming const... yes
checking whether char is unsigned... no
checking for inline... inline
checking for working volatile... yes
checking for typeof syntax and keyword spelling... __typeof__
checking for long long... yes
checking for off_t... yes
checking char bit... 8
checking size of int... 4
checking size of short... 2
checking size of long... 8
checking size of long long... 8
checking size of __int64... 0
checking size of off_t... 8
checking size of void*... 8
checking size of float... 4
checking size of double... 8
checking size of time_t... 8
checking size of clock_t... 8
checking packed struct attribute... x __attribute__((packed))
checking for printf prefix for long long... ll
checking for pid_t... yes
checking for convertible type of pid_t... INT
checking for uid_t... yes
checking for convertible type of uid_t... UINT
checking for gid_t... yes
checking for convertible type of gid_t... UINT
checking for time_t... yes
checking for convertible type of time_t... LONG
checking for dev_t... yes
checking for convertible type of dev_t... ULONG
checking for mode_t... yes
checking for convertible type of mode_t... UINT
checking for rlim_t... yes
checking for convertible type of rlim_t... ULONG
checking for off_t... (cached) yes
checking for convertible type of off_t... LONG
checking for clockid_t... yes
checking for convertible type of clockid_t... INT
checking for prototypes... yes
checking token paste string... ansi
checking stringization... #expr
checking string literal concatenation... yes
checking for variable length prototypes and stdarg.h... yes
checking for variable length macro... yes
checking for NORETURN function attribute... __attribute__ ((noreturn)) x
checking for DEPRECATED function attribute... __attribute__ ((deprecated)) x
checking for DEPRECATED_BY function attribute... __attribute__ ((deprecated("by "#n))) x
checking for DEPRECATED_TYPE type attribute... __attribute__ ((deprecated mesg)) x
checking for NOINLINE function attribute... __attribute__ ((noinline)) x
checking for WEAK function attribute... __attribute__ ((weak)) x
checking for stdcall function attribute... x
checking for cdecl function attribute... x
checking for fastcall function attribute... x
checking for FUNC_UNOPTIMIZED function attribute... __attribute__ ((optimize("O0"))) x
checking for FUNC_MINIMIZED function attribute... __attribute__ ((optimize("-Os","-fomit-frame-pointer"))) x
checking for function alias... alias
checking for __atomic builtins... yes
checking for __sync builtins... yes
checking for __builtin_unreachable... yes
checking for exported function attribute... __attribute__ ((visibility("default")))
checking for function name string predefined identifier... __func__
checking if enum over int is allowed... yes
checking whether sys_nerr is declared... yes
checking whether getenv is declared... yes
checking for size_t... yes
checking size of size_t... 8
checking size of ptrdiff_t... 8
checking for printf prefix for size_t... z
checking for printf prefix for ptrdiff_t... t
checking for struct stat.st_blksize... yes
checking for struct stat.st_blocks... yes
checking for struct stat.st_rdev... yes
checking size of struct stat.st_size... SIZEOF_OFF_T
checking size of struct stat.st_blocks... SIZEOF_OFF_T
checking size of struct stat.st_ino... SIZEOF_LONG
checking for struct stat.st_atim... yes
checking for struct stat.st_atimespec... no
checking for struct stat.st_atimensec... no
checking for struct stat.st_mtim... yes
checking for struct stat.st_mtimespec... no
checking for struct stat.st_mtimensec... no
checking for struct stat.st_ctim... yes
checking for struct stat.st_ctimespec... no
checking for struct stat.st_ctimensec... no
checking for struct stat.st_birthtimespec... no
checking for struct timeval... yes
checking size of struct timeval.tv_sec... SIZEOF_TIME_T
checking for struct timespec... yes
checking for struct timezone... yes
checking for clockid_t... (cached) yes
checking for fd_mask... yes
checking for int8_t... yes
checking size of int8_t... 1
checking for uint8_t... yes
checking size of uint8_t... 1
checking for int16_t... yes
checking size of int16_t... 2
checking for uint16_t... yes
checking size of uint16_t... 2
checking for int32_t... yes
checking size of int32_t... 4
checking for uint32_t... yes
checking size of uint32_t... 4
checking for int64_t... yes
checking size of int64_t... 8
checking for uint64_t... yes
checking size of uint64_t... 8
checking for intptr_t... yes
checking size of intptr_t... 8
checking for uintptr_t... yes
checking size of uintptr_t... 8
checking for ssize_t... yes
checking size of ssize_t... 8
checking for stack end address... __libc_stack_end
checking for uid_t in sys/types.h... (cached) yes
checking type of array argument to getgroups... gid_t
checking return type of signal handlers... void
checking for working alloca.h... yes
checking for alloca... yes
checking for dynamic size alloca... ok
checking for working memcmp... yes
checking for broken erfc of glibc-2.3.6 on IA64... no
checking for acosh... yes
checking for cbrt... yes
checking for crypt... yes
checking for dup2... yes
checking for erf... yes
checking for explicit_bzero... no
checking for ffs... yes
checking for finite... yes
checking for flock... yes
checking for hypot... yes
checking for isinf... yes
checking for isnan... yes
checking for lgamma_r... yes
checking for memmove... yes
checking for nextafter... yes
checking for setproctitle... no
checking for strchr... yes
checking for strerror... yes
checking for strlcat... no
checking for strlcpy... no
checking for strstr... yes
checking for tgamma... yes
checking sys/pstat.h usability... no
checking sys/pstat.h presence... no
checking for sys/pstat.h... no
checking for signbit... yes
checking for broken memmem... no
checking for pid_t... (cached) yes
checking vfork.h usability... no
checking vfork.h presence... no
checking for vfork.h... no
checking for fork... yes
checking for vfork... yes
checking for working fork... yes
checking for working vfork... (cached) yes
checking for __syscall... no
checking for _longjmp... yes
checking for _setjmp... yes
checking for _setjmpex... no
checking for atan2l... yes
checking for atan2f... yes
checking for chroot... yes
checking for chsize... no
checking for clock_gettime... no
checking for cosh... yes
checking for daemon... (cached) no
checking for dirfd... yes
checking for dl_iterate_phdr... yes
checking for dlopen... yes
checking for dladdr... yes
checking for dup... yes
checking for dup3... yes
checking for eaccess... yes
checking for endgrent... yes
checking for fchmod... yes
checking for fchown... yes
checking for fcntl... yes
checking for fdatasync... yes
checking for fgetattrlist... no
checking for fmod... yes
checking for fsync... yes
checking for ftruncate... yes
checking for ftruncate64... yes
checking for getattrlist... no
checking for getcwd... yes
checking for getgidx... no
checking for getgrnam... yes
checking for getgrnam_r... yes
checking for getgroups... yes
checking for getpgid... yes
checking for getpgrp... yes
checking for getpriority... yes
checking for getpwnam_r... yes
checking for getresgid... yes
checking for getresuid... yes
checking for getrlimit... yes
checking for getsid... yes
checking for gettimeofday... yes
checking for getuidx... no
checking for gmtime_r... yes
checking for initgroups... yes
checking for ioctl... yes
checking for isfinite... no
checking for issetugid... no
checking for killpg... yes
checking for lchmod... no
checking for lchown... yes
checking for link... yes
checking for llabs... yes
checking for lockf... yes
checking for log2... yes
checking for lstat... yes
checking for malloc_usable_size... yes
checking for malloc_size... no
checking for mblen... yes
checking for memalign... yes
checking for memset_s... no
checking for writev... yes
checking for memrchr... yes
checking for memmem... yes
checking for mkfifo... yes
checking for mknod... yes
checking for mktime... yes
checking for pipe2... yes
checking for poll... yes
checking for posix_fadvise... yes
checking for posix_memalign... yes
checking for ppoll... yes
checking for pread... yes
checking for qsort_r... yes
checking for readlink... yes
checking for round... yes
checking for sched_getaffinity... yes
checking for seekdir... yes
checking for select_large_fdset... no
checking for sendfile... yes
checking for setegid... yes
checking for setenv... yes
checking for seteuid... yes
checking for setgid... yes
checking for setgroups... yes
checking for setpgid... yes
checking for setpgrp... yes
checking for setregid... yes
checking for setresgid... yes
checking for setresuid... yes
checking for setreuid... yes
checking for setrgid... no
checking for setrlimit... yes
checking for setruid... no
checking for setsid... yes
checking for setuid... yes
checking for shutdown... yes
checking for sigaction... yes
checking for sigaltstack... yes
checking for sigprocmask... yes
checking for sinh... yes
checking for spawnv... no
checking for symlink... yes
checking for syscall... yes
checking for sysconf... yes
checking for tanh... yes
checking for telldir... yes
checking for timegm... yes
checking for times... yes
checking for truncate... yes
checking for truncate64... yes
checking for unsetenv... yes
checking for utimensat... yes
checking for utimes... yes
checking for wait4... yes
checking for waitpid... yes
checking if getcwd allocates buffer if NULL is given... yes
checking for __builtin_bswap16... no
checking for __builtin_bswap32... yes
checking for __builtin_bswap64... yes
checking for __builtin_clz... yes
checking for __builtin_clzl... yes
checking for __builtin_clzll... yes
checking for __builtin_choose_expr... yes
checking for __builtin_choose_expr_constant_p... no
checking for __builtin_types_compatible_p... yes
checking whether qsort_r is GNU version... yes
checking whether qsort_r is BSD version... no
checking whether atan2 handles Inf as C99... yes
checking for clock_gettime in -lrt... yes
checking for clock_getres... yes
checking for unsetenv returns a value... yes
checking for sigsetjmp as a macro or function... yes
checking whether struct tm is in sys/time.h or time.h... time.h
checking for struct tm.tm_zone... yes
checking for struct tm.tm_gmtoff... yes
checking for external int daylight... yes
checking for external timezone... long
checking for external altzone... no
checking for timezone... yes
checking whether timezone requires zero arguments... yes
checking for negative time_t for gmtime(3)... yes
checking for localtime(3) overflow correctly... yes
checking whether right shift preserve sign bit... yes
checking whether _SC_CLK_TCK is supported... yes
checking stack growing direction on x86_64... -1
checking for pthread_kill in -lthr... no
checking for pthread_kill in -lpthread... yes
checking for pthread_np.h... no
checking whether pthread_t is scalar type... yes
checking for sched_yield... yes
checking for pthread_attr_setinheritsched... yes
checking for pthread_attr_get_np... no
checking for pthread_attr_getstack... yes
checking for pthread_get_stackaddr_np... no
checking for pthread_get_stacksize_np... no
checking for thr_stksegment... no
checking for pthread_stackseg_np... no
checking for pthread_getthrds_np... no
checking for pthread_cond_init... yes
checking for pthread_condattr_setclock... yes
checking for pthread_condattr_init... yes
checking for pthread_sigmask... yes
checking for pthread_setname_np... yes
checking for pthread_set_name_np... no
checking for pthread_getattr_np... yes
checking for pthread_attr_init... yes
checking arguments of pthread_setname_np... (pthread_self(), name)
checking if mcontext_t is a pointer... no
checking for getcontext... yes
checking for setcontext... yes
checking if fork works with pthread... yes
checking whether ELF binaries are produced... yes
checking elf.h usability... yes
checking elf.h presence... yes
checking for elf.h... yes
checking elf_abi.h usability... no
checking elf_abi.h presence... no
checking for elf_abi.h... no
checking whether OS depend dynamic link works... yes
checking whether -Wl,-R. is accepted as LDFLAGS... yes
checking for backtrace... yes
checking for broken backtrace... no
checking valgrind/memcheck.h usability... no
checking valgrind/memcheck.h presence... no
checking for valgrind/memcheck.h... no
checking for strip... strip
checking whether -Wl,--no-undefined is accepted as LDFLAGS... yes
checking whether wrapper for LD_LIBRARY_PATH is needed... no
checking for __builtin_setjmp... yes with cast ()
checking for setjmp type... __builtin_setjmp
checking for prefix of external symbols... NONE
checking pthread.h usability... yes
checking pthread.h presence... yes
checking for pthread.h... yes

-->

````````````````````````

checking if make is GNU make... yes
checking for nroff... /usr/bin/nroff
.ext/include/x86_64-linux/ruby/config.h updated
configure: ruby library version = 2.3.0
configure: creating ./config.status
config.status: creating GNUmakefile
config.status: creating Makefile
config.status: creating ruby-2.3.pc

$ make
	CC = gcc
	LD = ld
	LDSHARED = gcc -shared
	CFLAGS = -O3 -fno-fast-math -ggdb3 -Wall -Wextra -Wno-unused-parameter -Wno-parentheses -Wno-long-long -Wno-missing-field-initializers -Wunused-variable -Wpointer-arith -Wwrite-strings -Wdeclaration-after-statement -Wimplicit-function-declaration -Wdeprecated-declarations -Wno-packed-bitfield-compat -std=iso9899:1999  -fPIC 
	XCFLAGS = -D_FORTIFY_SOURCE=2 -fstack-protector -fno-strict-overflow -fvisibility=hidden -DRUBY_EXPORT
	CPPFLAGS =   -I. -I.ext/include/x86_64-linux -I./include -I.
	DLDFLAGS = -Wl,-soname,libruby.so.2.3  -fstack-protector  
	SOLIBS = -lpthread -lrt -ldl -lcrypt -lm  
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/4.7/lto-wrapper
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Debian 4.7.2-5' --with-bugurl=file:///usr/share/doc/gcc-4.7/README.Bugs --enable-languages=c,c++,go,fortran,objc,obj-c++ --prefix=/usr --program-suffix=-4.7 --enable-shared --enable-linker-build-id --with-system-zlib --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --with-gxx-include-dir=/usr/include/c++/4.7 --libdir=/usr/lib --enable-nls --with-sysroot=/ --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --enable-gnu-unique-object --enable-plugin --enable-objc-gc --with-arch-32=i586 --with-tune=generic --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu
Thread model: posix
gcc version 4.7.2 (Debian 4.7.2-5) 
compiling main.c
compiling dmydln.c

````````````````````````

と受けて、

<!--
compiling miniinit.c
compiling dmyext.c
compiling miniprelude.c
copying dummy probes.h
compiling array.c
compiling bignum.c
compiling class.c
compiling compar.c
compiling complex.c
compiling dir.c
compiling dln_find.c
compiling encoding.c
compiling enum.c
compiling enumerator.c
compiling error.c
compiling eval.c
compiling load.c
compiling proc.c
compiling file.c
compiling gc.c
compiling hash.c
compiling inits.c
compiling io.c
compiling marshal.c
compiling math.c
compiling node.c
compiling numeric.c
compiling object.c
compiling pack.c
compiling parse.c
compiling process.c
compiling random.c
compiling range.c
compiling rational.c
compiling re.c
compiling regcomp.c
compiling regenc.c
compiling regerror.c
compiling regexec.c
compiling regparse.c
compiling regsyntax.c
compiling ruby.c
compiling safe.c
compiling signal.c
compiling sprintf.c
In file included from sprintf.c:1272:0:
vsnprintf.c: In function ‘BSD_vfprintf’:
vsnprintf.c:828:8: warning: comparison of unsigned expression < 0 is always false [-Wtype-limits]
vsnprintf.c:828:8: warning: comparison of unsigned expression < 0 is always false [-Wtype-limits]
compiling st.c
compiling strftime.c
compiling string.c
compiling struct.c
compiling symbol.c
compiling time.c
compiling transcode.c
compiling util.c
compiling variable.c
compiling version.c
compiling compile.c
compiling debug.c
compiling iseq.c
iseq.c: In function ‘rb_iseq_compile_with_option’:
iseq.c:636:8: warning: ‘ln’ may be used uninitialized in this function [-Wmaybe-uninitialized]
iseq.c:636:8: warning: ‘parse’ may be used uninitialized in this function [-Wmaybe-uninitialized]
iseq.c:638:11: warning: ‘type’ may be used uninitialized in this function [-Wmaybe-uninitialized]
iseq.c:638:11: warning: ‘label’ may be used uninitialized in this function [-Wmaybe-uninitialized]
compiling vm.c
compiling vm_dump.c
compiling vm_backtrace.c
compiling vm_trace.c
compiling thread.c
compiling cont.c
compiling enc/ascii.c
compiling enc/us_ascii.c
compiling enc/unicode.c
compiling enc/utf_8.c
compiling enc/trans/newline.c
compiling ./missing/explicit_bzero.c
compiling ./missing/setproctitle.c
compiling ./missing/strlcat.c
compiling ./missing/strlcpy.c
compiling addr2line.c
compiling dmyenc.c
linking miniruby
rbconfig.rb updated
generating enc.mk
compiling dln.c
compiling localeinit.c
creating verconf.h
verconf.h updated
compiling loadpath.c
compiling prelude.c
linking static-library libruby-static.a
verifying static-library libruby-static.a
linking shared-library libruby.so.2.3.0
generating encdb.h
encdb.h updated
making enc
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' に入ります
compiling ./enc/encdb.c
linking encoding encdb.so
compiling ./enc/big5.c
linking encoding big5.so
compiling ./enc/cp949.c
linking encoding cp949.so
compiling ./enc/emacs_mule.c
linking encoding emacs_mule.so
compiling ./enc/euc_jp.c
linking encoding euc_jp.so
compiling ./enc/euc_kr.c
linking encoding euc_kr.so
compiling ./enc/euc_tw.c
linking encoding euc_tw.so
compiling ./enc/gb2312.c
linking encoding gb2312.so
compiling ./enc/gb18030.c
linking encoding gb18030.so
compiling ./enc/gbk.c
linking encoding gbk.so
compiling ./enc/iso_8859_1.c
linking encoding iso_8859_1.so
compiling ./enc/iso_8859_2.c
linking encoding iso_8859_2.so
compiling ./enc/iso_8859_3.c
linking encoding iso_8859_3.so
compiling ./enc/iso_8859_4.c
linking encoding iso_8859_4.so
compiling ./enc/iso_8859_5.c
linking encoding iso_8859_5.so
compiling ./enc/iso_8859_6.c
linking encoding iso_8859_6.so
compiling ./enc/iso_8859_7.c
linking encoding iso_8859_7.so
compiling ./enc/iso_8859_8.c
linking encoding iso_8859_8.so
compiling ./enc/iso_8859_9.c
linking encoding iso_8859_9.so
compiling ./enc/iso_8859_10.c
linking encoding iso_8859_10.so
compiling ./enc/iso_8859_11.c
linking encoding iso_8859_11.so
compiling ./enc/iso_8859_13.c
linking encoding iso_8859_13.so
compiling ./enc/iso_8859_14.c
linking encoding iso_8859_14.so
compiling ./enc/iso_8859_15.c
linking encoding iso_8859_15.so
compiling ./enc/iso_8859_16.c
linking encoding iso_8859_16.so
compiling ./enc/koi8_r.c
linking encoding koi8_r.so
compiling ./enc/koi8_u.c
linking encoding koi8_u.so
compiling ./enc/shift_jis.c
linking encoding shift_jis.so
compiling ./enc/utf_16be.c
linking encoding utf_16be.so
compiling ./enc/utf_16le.c
linking encoding utf_16le.so
compiling ./enc/utf_32be.c
linking encoding utf_32be.so
compiling ./enc/utf_32le.c
linking encoding utf_32le.so
compiling ./enc/windows_31j.c
linking encoding windows_31j.so
compiling ./enc/windows_1250.c
linking encoding windows_1250.so
compiling ./enc/windows_1251.c
linking encoding windows_1251.so
compiling ./enc/windows_1252.c
linking encoding windows_1252.so
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' から出ます
making srcs under enc
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' に入ります
make[1]: `srcs' に対して行うべき事はありません.
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' から出ます
generating transdb.h
transdb.h updated
making trans
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' に入ります
compiling ./enc/trans/transdb.c
linking transcoder transdb.so
compiling ./enc/trans/big5.c
linking transcoder big5.so
compiling ./enc/trans/chinese.c
linking transcoder chinese.so
compiling ./enc/trans/ebcdic.c
linking transcoder ebcdic.so
compiling ./enc/trans/emoji.c
linking transcoder emoji.so
compiling ./enc/trans/emoji_iso2022_kddi.c
linking transcoder emoji_iso2022_kddi.so
compiling ./enc/trans/emoji_sjis_docomo.c
linking transcoder emoji_sjis_docomo.so
compiling ./enc/trans/emoji_sjis_kddi.c
linking transcoder emoji_sjis_kddi.so
compiling ./enc/trans/emoji_sjis_softbank.c
linking transcoder emoji_sjis_softbank.so
compiling ./enc/trans/escape.c
linking transcoder escape.so
compiling ./enc/trans/gb18030.c
linking transcoder gb18030.so
compiling ./enc/trans/gbk.c
linking transcoder gbk.so
compiling ./enc/trans/iso2022.c
linking transcoder iso2022.so
compiling ./enc/trans/japanese.c
linking transcoder japanese.so
compiling ./enc/trans/japanese_euc.c
linking transcoder japanese_euc.so
compiling ./enc/trans/japanese_sjis.c
linking transcoder japanese_sjis.so
compiling ./enc/trans/korean.c
linking transcoder korean.so
compiling ./enc/trans/single_byte.c
linking transcoder single_byte.so
compiling ./enc/trans/utf8_mac.c
linking transcoder utf8_mac.so
compiling ./enc/trans/utf_16_32.c
linking transcoder utf_16_32.so
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' から出ます
making encs
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' に入ります
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' から出ます
file2lastrev.rb: does not seem to be under a vcs: .
make: [.revision.time] エラー 1 (無視されました)
./revision.h unchanged
generating makefile exts.mk
configuring -test-/array/resize
configuring -test-/bignum
configuring -test-/bug-3571
configuring -test-/bug-5832
configuring -test-/bug_reporter
configuring -test-/class
configuring -test-/debug
configuring -test-/dln/empty
configuring -test-/exception
configuring -test-/fatal
configuring -test-/file
configuring -test-/float
configuring -test-/funcall
configuring -test-/gvl/call_without_gvl
configuring -test-/hash
configuring -test-/iseq_load
configuring -test-/iter
configuring -test-/load/dot.dot
configuring -test-/marshal/compat
configuring -test-/marshal/internal_ivar
configuring -test-/marshal/usr
configuring -test-/method
configuring -test-/notimplement
configuring -test-/num2int
configuring -test-/path_to_class
configuring -test-/popen_deadlock
configuring -test-/postponed_job
configuring -test-/printf
configuring -test-/proc
configuring -test-/rational
configuring -test-/recursion
configuring -test-/st/foreach
configuring -test-/st/numhash
configuring -test-/st/update
configuring -test-/string
configuring -test-/struct
configuring -test-/symbol
configuring -test-/time
configuring -test-/tracepoint
configuring -test-/typeddata
configuring -test-/wait_for_single_fd
configuring bigdecimal
configuring cgi/escape
configuring continuation
configuring coverage
configuring date
configuring dbm
Failed to configure dbm. It will not be installed.
configuring digest
configuring digest/bubblebabble
configuring digest/md5
configuring digest/rmd160
configuring digest/sha1
configuring digest/sha2
configuring etc
configuring fcntl
configuring fiber
configuring fiddle
configuring gdbm
Failed to configure gdbm. It will not be installed.
configuring io/console
configuring io/nonblock
configuring io/wait
configuring json
configuring json/generator
configuring json/parser
configuring mathn/complex
configuring mathn/rational
configuring nkf
configuring objspace
configuring openssl					← これ
configuring pathname
configuring psych
configuring pty
configuring racc/cparse
configuring rbconfig/sizeof
configuring readline
configuring ripper
missing bison; abort
Failed to configure ripper. It will not be installed.
configuring sdbm
configuring socket
configuring stringio
configuring strscan
configuring syslog
configuring thread
configuring tk
............
check struct members..
check libraries....
Use ActiveTcl libraries (if available).
Search tclConfig.sh and tkConfig.sh............................
Fail to find [tclConfig.sh, tkConfig.sh]
Use X11 libraries (or use TK_XINCLUDES/TK_XLIBSW information on tkConfig.sh).

Search tcl.h..
Search tk.h..Search Tcl library...........
Warning:: cannot find Tcl library. tcltklib will not be compiled (tcltklib is disabled on your Ruby. That is, Ruby/Tk will not work). Please check configure options.

Can't find proper Tcl/Tk libraries. So, can't make tcltklib.so which is required by Ruby/Tk.
If you have Tcl/Tk libraries on your environment, you may be able to use them with configure options (see ext/tk/README.tcltklib).
At present, Tcl/Tk8.6 is not supported. Although you can try to use Tcl/Tk8.6 with configure options, it will not work correctly. I recommend you to use Tcl/Tk8.5 or 8.4.
Failed to configure tk. It will not be installed.
Failed to configure tk/tkutil. It will not be installed.
configuring zlib
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' に入ります
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/array/resize' に入ります
compiling resize.c
linking shared-object -test-/array/resize.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/array/resize' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bignum' に入ります
compiling bigzero.c
compiling init.c
compiling str2big.c
compiling div.c
compiling intpack.c
compiling mul.c
compiling big2str.c
linking shared-object -test-/bignum.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bignum' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bug-3571' に入ります
compiling bug.c
linking shared-object -test-/bug-3571/bug.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bug-3571' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bug-5832' に入ります
compiling bug.c
linking shared-object -test-/bug-5832/bug.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bug-5832' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bug_reporter' に入ります
compiling bug_reporter.c
linking shared-object -test-/bug_reporter/bug_reporter.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/bug_reporter' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/class' に入ります
compiling init.c
compiling class2name.c
linking shared-object -test-/class.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/class' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/debug' に入ります
compiling init.c
compiling inspector.c
compiling profile_frames.c
linking shared-object -test-/debug.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/debug' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/dln/empty' に入ります
compiling empty.c
linking shared-object -test-/dln/empty.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/dln/empty' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/exception' に入ります
compiling init.c
compiling ensured.c
compiling enc_raise.c
compiling dataerror.c
linking shared-object -test-/exception.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/exception' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/fatal' に入ります
compiling rb_fatal.c
linking shared-object -test-/fatal/rb_fatal.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/fatal' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/file' に入ります
compiling init.c
compiling stat.c
compiling fs.c
linking shared-object -test-/file.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/file' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/float' に入ります
compiling init.c
compiling nextafter.c
linking shared-object -test-/float.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/float' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/funcall' に入ります
compiling passing_block.c
linking shared-object -test-/funcall/funcall.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/funcall' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/gvl/call_without_gvl' に入ります
compiling call_without_gvl.c
linking shared-object -test-/gvl/call_without_gvl.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/gvl/call_without_gvl' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/hash' に入ります
compiling init.c
compiling delete.c
linking shared-object -test-/hash.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/hash' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/iseq_load' に入ります
compiling iseq_load.c
linking shared-object -test-/iseq_load/iseq_load.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/iseq_load' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/iter' に入ります
compiling yield.c
compiling init.c
compiling break.c
linking shared-object -test-/iter.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/iter' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/load/dot.dot' に入ります
compiling dot.dot.c
linking shared-object -test-/load/dot.dot/dot.dot.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/load/dot.dot' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/marshal/compat' に入ります
compiling usrcompat.c
linking shared-object -test-/marshal/compat.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/marshal/compat' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/marshal/internal_ivar' に入ります
compiling internal_ivar.c
linking shared-object -test-/marshal/internal_ivar.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/marshal/internal_ivar' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/marshal/usr' に入ります
compiling usrmarshal.c
linking shared-object -test-/marshal/usr.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/marshal/usr' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/method' に入ります
compiling arity.c
compiling init.c
linking shared-object -test-/method.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/method' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/notimplement' に入ります
compiling bug.c
linking shared-object -test-/notimplement.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/notimplement' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/num2int' に入ります
compiling num2int.c
linking shared-object -test-/num2int/num2int.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/num2int' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/path_to_class' に入ります
compiling path_to_class.c
linking shared-object -test-/path_to_class/path_to_class.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/path_to_class' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/popen_deadlock' に入ります
compiling infinite_loop_dlsym.c
linking shared-object -test-/popen_deadlock/infinite_loop_dlsym.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/popen_deadlock' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/postponed_job' に入ります
compiling postponed_job.c
linking shared-object -test-/postponed_job.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/postponed_job' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/printf' に入ります
compiling printf.c
linking shared-object -test-/printf.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/printf' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/proc' に入ります
compiling init.c
compiling receiver.c
compiling super.c
linking shared-object -test-/proc.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/proc' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/rational' に入ります
compiling rat.c
linking shared-object -test-/rational.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/rational' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/recursion' に入ります
compiling recursion.c
linking shared-object -test-/recursion.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/recursion' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/st/foreach' に入ります
compiling foreach.c
linking shared-object -test-/st/foreach.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/st/foreach' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/st/numhash' に入ります
compiling numhash.c
linking shared-object -test-/st/numhash.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/st/numhash' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/st/update' に入ります
compiling update.c
linking shared-object -test-/st/update.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/st/update' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/string' に入ります
compiling enc_associate.c
compiling init.c
compiling modify.c
compiling enc_str_buf_cat.c
compiling cstr.c
compiling ellipsize.c
compiling nofree.c
compiling qsort.c
compiling set_len.c
compiling coderange.c
compiling normalize.c
compiling fstring.c
linking shared-object -test-/string.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/string' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/struct' に入ります
compiling init.c
compiling member.c
linking shared-object -test-/struct.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/struct' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/symbol' に入ります
compiling init.c
compiling type.c
linking shared-object -test-/symbol.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/symbol' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/time' に入ります
compiling init.c
compiling new.c
linking shared-object -test-/time.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/time' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/tracepoint' に入ります
compiling gc_hook.c
compiling tracepoint.c
linking shared-object -test-/tracepoint.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/tracepoint' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/typeddata' に入ります
compiling typeddata.c
linking shared-object -test-/typeddata/typeddata.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/typeddata' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/wait_for_single_fd' に入ります
compiling wait_for_single_fd.c
linking shared-object -test-/wait_for_single_fd/wait_for_single_fd.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/-test-/wait_for_single_fd' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/bigdecimal' に入ります
compiling bigdecimal.c
linking shared-object bigdecimal.so
installing default bigdecimal libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/bigdecimal' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/cgi/escape' に入ります
compiling escape.c
escape.c: In function ‘cgiesc_escape_html’:
escape.c:40:11: warning: ‘dest’ may be used uninitialized in this function [-Wmaybe-uninitialized]
linking shared-object cgi/escape.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/cgi/escape' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/continuation' に入ります
compiling continuation.c
linking shared-object continuation.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/continuation' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/coverage' に入ります
compiling coverage.c
linking shared-object coverage.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/coverage' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/date' に入ります
compiling date_parse.c
compiling date_strftime.c
compiling date_strptime.c
compiling date_core.c
linking shared-object date_core.so
installing default date_core libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/date' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/dbm' に入ります
make[2]: `all' に対して行うべき事はありません.
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/dbm' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest' に入ります
compiling digest.c
linking shared-object digest.so
installing digest libraries
installing default digest libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/bubblebabble' に入ります
compiling bubblebabble.c
linking shared-object digest/bubblebabble.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/bubblebabble' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/md5' に入ります
compiling md5init.c
linking shared-object digest/md5.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/md5' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/rmd160' に入ります
compiling rmd160init.c
linking shared-object digest/rmd160.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/rmd160' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/sha1' に入ります
compiling sha1init.c
linking shared-object digest/sha1.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/sha1' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/sha2' に入ります
compiling sha2init.c
linking shared-object digest/sha2.so
installing default sha2 libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/digest/sha2' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/etc' に入ります
compiling etc.c
linking shared-object etc.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/etc' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fcntl' に入ります
compiling fcntl.c
linking shared-object fcntl.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fcntl' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiber' に入ります
compiling fiber.c
linking shared-object fiber.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiber' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle' に入ります
compiling function.c
compiling handle.c
compiling fiddle.c
compiling closure.c
compiling pointer.c
compiling conversions.c
make[3]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1' に入ります
make 'AR_FLAGS=' 'CC_FOR_BUILD=' 'CFLAGS=-O3 -fno-fast-math -ggdb3   -fPIC -Wall -fexceptions' 'CXXFLAGS=-O3 -fno-fast-math -ggdb3 ' 'CFLAGS_FOR_BUILD=' 'CFLAGS_FOR_TARGET=' 'INSTALL=/usr/bin/install -c' 'INSTALL_DATA=/usr/bin/install -c -m 644' 'INSTALL_PROGRAM=/usr/bin/install -c' 'INSTALL_SCRIPT=/usr/bin/install -c' 'JC1FLAGS=' 'LDFLAGS=-L. -fstack-protector -rdynamic -Wl,-export-dynamic  -L../../.. -Wl,-R/usr/local/lib -L/usr/local/lib -lruby' 'LIBCFLAGS=' 'LIBCFLAGS_FOR_TARGET=' 'MAKE=make' 'MAKEINFO=/bin/bash /home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/missing makeinfo ' 'PICFLAG=' 'PICFLAG_FOR_TARGET=' 'RUNTESTFLAGS=' 'SHELL=/bin/bash' 'exec_prefix=/usr/local' 'infodir=/usr/local/share/info' 'libdir=/usr/local/lib' 'mandir=/usr/local/share/man' 'prefix=/usr/local' 'AR=ar' 'AS=as' 'CC=gcc' 'CXX=g++' 'LD=ld -m elf_x86_64' 'NM=nm' 'RANLIB=ranlib' 'DESTDIR=' all-recursive
make[4]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1' に入ります
Making all in include
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/include' に入ります
make[5]: `all' に対して行うべき事はありません.
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/include' から出ます
Making all in testsuite
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/testsuite' に入ります
make[5]: `all' に対して行うべき事はありません.
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/testsuite' から出ます
Making all in man
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/man' に入ります
make[5]: `all' に対して行うべき事はありません.
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1/man' から出ます
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1' に入ります
  CC       src/prep_cif.lo
  CC       src/types.lo
  CC       src/raw_api.lo
  CC       src/java_raw_api.lo
  CC       src/closures.lo
  CC       src/x86/ffi64.lo
  CPPAS    src/x86/unix64.lo
  CC       src/x86/ffi.lo
  CPPAS    src/x86/sysv.lo
  CCLD     libffi_convenience.la
  CCLD     libffi.la
make[5]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1' から出ます
make[4]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1' から出ます
make[3]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle/libffi-3.2.1' から出ます
linking shared-object fiddle.so
installing default fiddle libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/fiddle' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/gdbm' に入ります
make[2]: `all' に対して行うべき事はありません.
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/gdbm' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/io/console' に入ります
compiling console.c
linking shared-object io/console.so
installing default console libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/io/console' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/io/nonblock' に入ります
compiling nonblock.c
linking shared-object io/nonblock.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/io/nonblock' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/io/wait' に入ります
compiling wait.c
linking shared-object io/wait.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/io/wait' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/json' に入ります
installing default libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/json' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/json/generator' に入ります
compiling generator.c
linking shared-object json/ext/generator.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/json/generator' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/json/parser' に入ります
compiling parser.c
linking shared-object json/ext/parser.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/json/parser' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/mathn/complex' に入ります
compiling complex.c
linking shared-object mathn/complex.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/mathn/complex' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/mathn/rational' に入ります
compiling rational.c
linking shared-object mathn/rational.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/mathn/rational' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/nkf' に入ります
compiling nkf.c
linking shared-object nkf.so
installing default nkf libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/nkf' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/objspace' に入ります
compiling objspace.c
compiling objspace_dump.c
compiling object_tracing.c
linking shared-object objspace.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/objspace' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/openssl' に入ります		← これ
compiling ossl_ssl.c
compiling ossl_config.c
compiling ossl_digest.c
compiling ossl_x509name.c
compiling ossl_hmac.c
compiling ossl_x509.c
compiling ossl_engine.c
compiling ossl.c
compiling ossl_pkcs5.c
compiling ossl_pkcs7.c
compiling ossl_x509store.c
compiling ossl_x509revoked.c
compiling ossl_x509req.c
compiling ossl_pkey_ec.c
compiling ossl_cipher.c
compiling ossl_x509crl.c
compiling ossl_bio.c
compiling ossl_asn1.c
compiling ossl_x509attr.c
compiling ossl_pkey_rsa.c
compiling ossl_pkey_dsa.c
compiling ossl_ns_spki.c
compiling ossl_pkey.c
compiling openssl_missing.c
compiling ossl_bn.c
compiling ossl_ocsp.c
compiling ossl_ssl_session.c
compiling ossl_pkcs12.c
compiling ossl_x509cert.c
compiling ossl_pkey_dh.c
compiling ossl_x509ext.c
compiling ossl_rand.c
linking shared-object openssl.so
installing default openssl libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/openssl' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/pathname' に入ります
compiling pathname.c
linking shared-object pathname.so
installing default pathname libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/pathname' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/psych' に入ります
compiling psych_yaml_tree.c
compiling psych_emitter.c
compiling psych_to_ruby.c
compiling psych.c
compiling psych_parser.c
compiling ../.././ext/psych/yaml/scanner.c
compiling ../.././ext/psych/yaml/parser.c
compiling ../.././ext/psych/yaml/api.c
compiling ../.././ext/psych/yaml/emitter.c
compiling ../.././ext/psych/yaml/dumper.c
compiling ../.././ext/psych/yaml/loader.c
compiling ../.././ext/psych/yaml/reader.c
compiling ../.././ext/psych/yaml/writer.c
linking shared-object psych.so
installing default psych libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/psych' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/pty' に入ります
compiling pty.c
linking shared-object pty.so
installing default pty libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/pty' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/racc/cparse' に入ります
compiling cparse.c
linking shared-object racc/cparse.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/racc/cparse' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/rbconfig/sizeof' に入ります
compiling sizes.c
linking shared-object rbconfig/sizeof.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/rbconfig/sizeof' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/readline' に入ります
compiling readline.c
linking shared-object readline.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/readline' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/ripper' に入ります
make[2]: `all' に対して行うべき事はありません.
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/ripper' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/sdbm' に入ります
compiling init.c
compiling _sdbm.c
linking shared-object sdbm.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/sdbm' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/socket' に入ります
compiling init.c
compiling constants.c
compiling basicsocket.c
compiling socket.c
compiling ipsocket.c
compiling tcpsocket.c
compiling tcpserver.c
compiling sockssocket.c
compiling udpsocket.c
compiling unixsocket.c
compiling unixserver.c
compiling option.c
compiling ancdata.c
compiling raddrinfo.c
compiling ifaddr.c
linking shared-object socket.so
installing default socket libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/socket' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/stringio' に入ります
compiling stringio.c
linking shared-object stringio.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/stringio' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/strscan' に入ります
compiling strscan.c
linking shared-object strscan.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/strscan' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/syslog' に入ります
compiling syslog.c
linking shared-object syslog.so
installing default syslog libraries
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/syslog' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/thread' に入ります
compiling thread.c
linking shared-object thread.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/thread' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/tk' に入ります
make[2]: `all' に対して行うべき事はありません.
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/tk' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/tk/tkutil' に入ります
make[2]: `all' に対して行うべき事はありません.
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/tk/tkutil' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/zlib' に入ります
compiling zlib.c
linking shared-object zlib.so
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0/ext/zlib' から出ます
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' に入ります
linking shared-library libruby.so.2.3.0
linking ruby
make[2]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' から出ます
make[1]: ディレクトリ `/home/hayashiisme/src/ruby-2.3.0' から出ます
-->


````````````````````````

Generating RDoc documentation
Parsing sources...
100% [944/944]  vsnprintf.c                                                                    

Generating RI format into /home/hayashiisme/src/ruby-2.3.0/.ext/rdoc...

  Files:        944

  Classes:     1401 ( 576 undocumented)
  Modules:      280 ( 110 undocumented)
  Constants:   2171 ( 604 undocumented)
  Attributes:  1144 ( 255 undocumented)
  Methods:    10511 (2230 undocumented)

  Total:      15507 (3775 undocumented)
   75.66% documented

  Elapsed: 216.6s


````````````````````````

で、

````````````````````````

$ make install

````````````````````````

で終了。


***→ 「[GitHub Pages導入: Windowsでの環境構築](github-pages-03.html)」へ続く***

Qiitaにストックした記事をベースに手を動かす。

