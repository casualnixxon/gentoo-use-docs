# dev-libs/elfutils
### bzip2
This enables `--with-bzlib` configure option. Doing so will compile `libdwfl` with BZip2 compression support. This is required for dealing with kernel and modules compressed using bz2.

This flag can be safely disabled if kernel or modules aren't compressed using aforementioned formats.

### lzma
This flag enables `--with-lzma` configure option. Doing so will compile `libdwfl` with LZMA compression support. This is required for dealing with kernel and modules compressed using LZMA or XZ.

This flag can be safely disabled if kernel or modules aren't compressed using aforementioned formats.

### nls
This will pass `--enable-nls` option to configure script. Enabling this flag will build and install translation files for variety of languages. This will enable localized messages, prompts, formats, etc.

It is safe to disable this flag if there is no need to support languages other than English.

### static-libs
When this flag is disabled ebuild will patch Makefile for `libasm`, `libdw` and `libelf` in order to prevent building and installing static `.a` libraries.

These libraries aren't normally required, except for some special use-cases of prelinking or development that requires static library. There are a few packages in the portage tree that require this flag to be set.

It's safe to disable this flag, unless there is a plan to deal with one or more use cases described above.

### test
This flag does two things:

- it appends `-g` (debugging) flag into `CFLAGS` for compiler because of [#407135](https://bugs.gentoo.org/407135).
- it executes `check` make target in order to run regression test suite.

Running tests will extend build time. It is also recommended to re-emerge this package without this flag enabled, otherwise installed libraries and binaries will have debugging information attached.

This flag is here mostly for debugging and should not be enabled by average user or on production systems.

### threads
This will pass `--enable-thread-safety` option to configure script. Subsequently this results in thread-safe versions of the elfutils libraries being built and installed.

This is **EXPERIMENTAL** feature and no packages in portage are depending on it being set. However some packages will enable threading mode for themselves if they detect this flag being set on `elfutils` package.

It is not recommended to enable this flag, especially on production systems.

### utils
Disabling this flag removes all binaries generated by the build system from installation. This means only libraries will be installed and no tools like `eu-elflint`, `eu-size`, `eu-readelf` and so on.

This flag can be safely disabled, because no packages in portage tree dependent on it. Developers might want to keep this flag enabled if they use tools provided.