userspace_c_args = [
  '-m80387', '-msse', '-msse2', '-mno-avx', '-mno-avx2',
  '-D__USER__',
]

if get_option('debug')
  userspace_c_args += ['-DMEMORY_GUARDS']
endif

libc_lib = static_library(
  'c',
  '__environ.c',
  '_start.c',
  'assert.c',
  'dirent.c',
  'ext.c',
  'fcntl.c',
  'getenv.c',
  'getopt.c',
  'longjmp.S',
  'math.c',
  'printf.c',
  'pwd.c',
  'reboot.c',
  'setenv.c',
  'setjmp.S',
  'signal.c',
  'sigsetjmp.S',
  'stdio.c',
  'stdlib.c',
  'string.c',
  'sys_ioctl.c',
  'sys_mman.c',
  'sys_ptrace.c',
  'sys_stat.c',
  'sys_uio.c',
  'sys_wait.c',
  'termios.c',
  'time.c',
  'umalloc.c',
  'unistd.c',
  c_args: userspace_c_args,
  include_directories: [global_include, 'include'],
)

libc_dep = declare_dependency(
  link_with: [libc_lib],
  include_directories: [global_include, 'include'],
  compile_args: userspace_c_args,
)

userspace_bindings_lib = static_library(
  'userspace_bindings',
  structured_sources([
    'rust/userspace_bindings/src/lib.rs',
    rust.bindgen(
      input: 'rust/userspace_bindings/wrapper.h',
      output: 'bindings.rs',
      include_directories: global_include,
      args: [
        '--use-core',
        '--constified-enum-module', '.*',
        '--builtins',
        '--with-derive-default',
        '--rust-edition', get_option('rust_std'),
        '--override-abi', '.*=C',
        '--wrap-unsafe-ops',
        '--flexarray-dst',
        '--rust-target', 'nightly',
        '--wrap-static-fns',
        '--translate-enum-integer-types',
        '--conservative-inline-namespaces',
        '--no-hash', '.*',
        '--formatter', 'rustfmt',
        '--enable-function-attribute-detection',
      ],
      c_args: [
        '-D__USER__=1',
        '-fno-builtin',
      ]
    )
  ]),
  dependencies: [spin_dep],
)

gui_lib = static_library(
  'gui',
  'rust/gui/src/lib.rs',
  link_with: [userspace_bindings_lib],
  dependencies: [spin_dep],
  rust_abi: 'c',
)

pci_lib = static_library(
  'pci',
  'rust/pci/src/lib.rs',
  link_with: [userspace_bindings_lib],
  dependencies: [pci_ids_dep],
  rust_abi: 'c',
)

subdir('programs')
