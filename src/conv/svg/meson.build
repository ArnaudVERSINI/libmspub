pub2xhtml = executable(
  'pub2xhtml',
  'pub2xhtml.cpp',
  include_directories: top_inc,
  dependencies: [libmspub_dep, revenge_stream_dep, icu_dep],
  cpp_args: ['-DVERSION="@0@"'.format(meson.project_version())],
  install: true,
)
