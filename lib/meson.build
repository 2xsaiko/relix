sharedlib_lib = static_library(
  'shared',
  'ctype.c',
  'qsort.c',
  'queue.c',
  'ring_buffer.c',
  'search.c',
  include_directories: [global_include],
)

sharedlib_dep = declare_dependency(
  link_with: [sharedlib_lib],
  include_directories: [global_include],
)
