project(
  'libmspub',
  'cpp',
  version: '0.1.6',
  license: 'MPL-2.0',
  meson_version: '>=0.53.0',
  default_options: [
    'cpp_std=c++11',
    'default_library=shared',
    'warning_level=2',
    'buildtype=release',
  ],
)

mspub_version = meson.project_version().split('.')
mspub_major_version = mspub_version[0]
mspub_minor_version = mspub_version[1]
mspub_micro_version = mspub_version[2]

cc = meson.get_compiler('cpp')

is_msvc = cc.get_argument_syntax() == 'msvc'
is_windows = host_machine.system() == 'windows'

boost_headers = [
  'boost/cstdint.hpp',
  'boost/multi_array.hpp',
  'boost/numeric/conversion/cast.hpp',
  'boost/optional.hpp',
]
foreach h : boost_headers
  if not cc.has_header(h)
    error('Required boost header ' + h + ' not found. Install boost')
  endif
endforeach

revenge_dep = dependency('librevenge-0.0', version: '>= 0.0.1')
zlib_dep = dependency('zlib')
icu_dep = dependency('icu-i18n')

enable_tools = get_option('tools')
enable_fuzzers = get_option('fuzzers')

if enable_tools or enable_fuzzers
  revenge_stream_dep = dependency('librevenge-stream-0.0')
  revenge_generators_dep = dependency('librevenge-generators-0.0')
endif

if get_option('debug')
  add_project_arguments('-DDEBUG', language: 'cpp')
else
  add_project_arguments('-DNDEBUG', language: 'cpp')
endif

if get_option('werror')
  add_project_arguments(cc.get_supported_arguments('-Werror'), language: 'cpp')
endif

if not is_msvc and not is_windows
  if cc.has_argument('-fvisibility=hidden')
    add_project_arguments('-fvisibility=hidden', '-DLIBMSPUB_VISIBILITY', language: 'cpp')
  endif
endif

top_inc = include_directories('inc')

subdir('inc')
subdir('src/lib')
if enable_tools
  subdir('src/conv')
endif
if enable_fuzzers
  subdir('src/fuzz')
endif

if get_option('docs') and not is_windows
  doxygen = find_program('doxygen', required: false)
  if doxygen.found()
    subdir('docs')
  else
    message('Could not find doxygen in your PATH; the documentation will not be built.')
  endif
endif

astyle = find_program('astyle', required: false)
if astyle.found()
  run_target(
    'astyle',
    command: [astyle, '--options=astyle.options', 'src/lib/*.cpp', 'src/lib/*.h', 'src/conv/*/*.cpp', 'inc/libmspub/*.h'],
  )
endif
