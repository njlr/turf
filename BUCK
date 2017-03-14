def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

TURF_CONFIG_H = """
#define TURF_HAS_STDINT 1
#define TURF_PREFER_CPP11 0
#define TURF_WITH_BOOST 0
#define TURF_PREFER_BOOST 0
#define TURF_WITH_EXCEPTIONS 0
#define TURF_HAS_NOEXCEPT 1
#define TURF_HAS_CONSTEXPR 1
#define TURF_HAS_OVERRIDE 1
#define TURF_HAS_LONG_LONG 1
#define TURF_HAS_STATIC_ASSERT 1
#define TURF_HAS_MOVE 1
#define TURF_REPLACE_OPERATOR_NEW 1
#define TURF_USE_DLMALLOC 0
#define TURF_DLMALLOC_DEBUG_CHECKS 0
#define TURF_DLMALLOC_FAST_STATS 0

#include \\"turf_userconfig.h\\"
"""

genrule(
  name = 'turf_userconfig.h',
  out = 'turf_userconfig.h',
  cmd = 'touch $OUT',
)

genrule(
  name = 'turf_config.h',
  out = 'turf_config.h',
  cmd = 'echo "' + TURF_CONFIG_H + '" > $OUT',
)

cxx_library(
  name = 'turf',
  header_namespace = '',
  exported_headers = merge_dicts(subdir_glob([
    ('', 'turf/**/*.h'),
    ('', 'turf/**/*.inc'),
  ]),
  {
    'turf_userconfig.h': ':turf_userconfig.h',
    'turf_config.h': ':turf_config.h',
  }),
  srcs = glob([
    'turf/**/*.cpp',
  ]),
  compiler_flags = [
    '-std=c++11',
  ],
  visibility = [
    'PUBLIC',
  ],
)
