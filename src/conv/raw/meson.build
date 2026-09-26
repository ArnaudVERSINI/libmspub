pub2raw = executable(
  'pub2raw',
  'pub2raw.cpp',
  include_directories: top_inc,
  dependencies: [libmspub_dep, revenge_stream_dep, revenge_generators_dep, icu_dep],
  cpp_args: [
    '-DPACKAGE="libmspub"',
    '-DVERSION="@0@"'.format(meson.project_version()),
  ],
  install: true,
)
