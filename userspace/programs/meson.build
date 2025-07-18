programs_link_args = [
  '-Wl,-z,noexecstack', '-Wl,-O1', '-Wl,-N,-e,_start', '-Wl,--section-start=.text=0x1000',
]

programs = []

foreach program : [
  '[', 'big', 'cat', 'chmod', 'date', 'donut', 'echo', 'env', 'errno',
  'fopentest', 'forkexec', 'forktest', 'fuzzclose', 'getty', 'grep', 'init',
  'kill', 'ln', 'login', 'ls', 'mkdir', 'mkfifo', 'mv', 'pipetest', 'poll',
  'prottest', 'ptrace', 'pwd', 'readelf', 'reader', 'readlink', 'reboot', 'rm',
  'scrinfo', 'setjmp', 'sh', 'sighandles', 'sleep', 'stressfs', 'syscalltest',
]
  programs += [
    executable(
      program,
      '@0@.c'.format(program),
      link_args: programs_link_args,
      dependencies: [sharedlib_dep, libc_dep]
    )
  ]
endforeach

programs += [
  executable(
    'lspci',
    'lspci.c',
    link_args: programs_link_args,
    dependencies: [sharedlib_dep, libc_dep],
    link_with: [pci_lib, gui_lib],
  ),
  executable(
    'draw',
    'draw.c',
    link_args: programs_link_args,
    dependencies: [sharedlib_dep, libc_dep],
    link_with: [gui_lib],
  ),
  executable(
    'fps',
    'fps.c',
    link_args: programs_link_args,
    dependencies: [sharedlib_dep, libc_dep],
    link_with: [gui_lib],
  )
]
