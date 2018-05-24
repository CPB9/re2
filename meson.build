project('re2', ['cpp'], default_options : ['cpp_std=c++11'])

cc = meson.get_compiler('cpp')

cflags = []

if cc.get_id() == 'msvc'
  cflags += '/wd4100'
  cflags += '/wd4201'
  cflags += '/wd4456'
  cflags += '/wd4457'
  cflags += '/wd4702'
  cflags += '/wd4815'
  cflags += '/utf-8'
endif

if host_machine.system() == 'windows'
  cflags += '-DUNICODE'
  cflags += '-D_UNICODE'
  cflags += '-DSTRICT'
  cflags += '-DNOMINMAX'
  cflags += '-D_CRT_SECURE_NO_WARNINGS'
  cflags += '-D_SCL_SECURE_NO_WARNINGS'
endif

thread_dep = dependency('threads', required : true)
deps = [thread_dep]

src = [
  're2/bitstate.cc',
  're2/compile.cc',
  're2/dfa.cc',
  're2/filtered_re2.cc',
  're2/mimics_pcre.cc',
  're2/nfa.cc',
  're2/onepass.cc',
  're2/parse.cc',
  're2/perl_groups.cc',
  're2/prefilter.cc',
  're2/prefilter_tree.cc',
  're2/prog.cc',
  're2/re2.cc',
  're2/regexp.cc',
  're2/set.cc',
  're2/simplify.cc',
  're2/stringpiece.cc',
  're2/tostring.cc',
  're2/unicode_casefold.cc',
  're2/unicode_groups.cc',
  'util/rune.cc',
  'util/strutil.cc',
]

re2_lib = static_library('re2',
  name_prefix : 'lib',
  sources : src,
  include_directories: include_directories('.'),
  dependencies: deps,
  cpp_args: cflags,
)

re2_dep = declare_dependency(
  link_with : re2_lib,
  include_directories: include_directories('.', is_system : true),
  dependencies: deps,
)

