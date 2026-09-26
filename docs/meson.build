doxygen_dir = meson.current_source_dir() / 'doxygen'

run_target(
  'docs',
  command: [
    find_program('python3'),
    '-c',
    'import os, subprocess, sys; os.chdir(sys.argv[1]); sys.exit(subprocess.run([sys.argv[2], "doxygen.cfg"]).returncode)',
    doxygen_dir,
    doxygen,
  ],
)
