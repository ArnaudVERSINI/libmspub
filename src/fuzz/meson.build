pubfuzzer = executable(
  'pubfuzzer',
  'pubfuzzer.cpp',
  include_directories: top_inc,
  dependencies: [libmspub_dep, revenge_stream_dep, revenge_generators_dep],
  link_args: ['-lFuzzingEngine'],
  install: false,
)
