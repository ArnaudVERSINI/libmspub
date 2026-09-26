libmspub_sources = files(
  'ColorReference.cpp',
  'Coordinate.cpp',
  'Dash.cpp',
  'Fill.cpp',
  'MSPUBCollector.cpp',
  'MSPUBDocument.cpp',
  'MSPUBMetaData.cpp',
  'MSPUBParser.cpp',
  'MSPUBParser2k.cpp',
  'MSPUBParser97.cpp',
  'PolygonUtils.cpp',
  'Shadow.cpp',
  'ShapeGroupElement.cpp',
  'VectorTransformation2D.cpp',
  'libmspub_utils.cpp',
)

lt_current = mspub_major_version.to_int() * 100 + mspub_minor_version.to_int()
lt_age = 0
libmspub_soversion = lt_current - lt_age
libmspub_full_version = '@0@.@1@.@2@'.format(libmspub_soversion, mspub_micro_version.to_int(), lt_age)

libmspub_lib = library(
  'mspub-' + mspub_major_version + '.' + mspub_minor_version,
  libmspub_sources,
  include_directories: top_inc,
  dependencies: [revenge_dep, zlib_dep, icu_dep],
  cpp_args: ['-DLIBMSPUB_BUILD=1'],
  version: libmspub_full_version,
  soversion: libmspub_soversion,
  install: true,
)

libmspub_dep = declare_dependency(
  link_with: libmspub_lib,
  include_directories: top_inc,
)

pkg = import('pkgconfig')

pkg.generate(
  libmspub_lib,
  description: 'Library for parsing the Microsoft Publisher file format structure',
  requires: ['librevenge-0.0'],
  requires_private: ['icu-i18n', 'zlib'],
)
