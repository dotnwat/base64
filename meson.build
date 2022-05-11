project('base64', 'c', default_options: ['c_std=c99'])

if get_option('enable_openmp')
  add_project_arguments('-fopenmp', language: 'c')
endif

codecs = ['avx', 'avx2', 'neon32', 'neon64', 'ssse3', 'sse41', 'sse42']

subdir('lib')

inc = include_directories('lib')

libs = []
foreach codec : codecs
  lib = static_library(codec,
    f'lib/arch/@codec@/codec.c', config_h,
    c_args: get_option(f'@codec@_flags'),
    include_directories: inc)
  libs += [lib]
endforeach

base64 = static_library('base64',
  'lib/arch/generic/codec.c',
  'lib/lib.c',
  'lib/codec_choose.c',
  'lib/tables/tables.c',
  config_h,
  include_directories: inc,
  link_whole: libs)

base64_dep = declare_dependency(
  include_directories: include_directories('include'),
  link_with: base64)
