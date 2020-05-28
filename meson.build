project('fidoconf','c', version:'1.9.0')

cc = meson.get_compiler('c')

link_args = []
compile_args = []

if cc.get_id() == 'msvc'
  add_project_arguments(
    '-D_CRT_SECURE_NO_DEPRECATE',
    '-D_CRT_NONSTDC_NO_DEPRECATE', 
    '-DWIN32',
    '-D_WINDOWS',
    '-D_CONSOLE',
    language : 'c')
  if get_option('default_library') != 'static'
    add_project_arguments('-D_DLL', '-D_MAKE_DLL', language : 'c')
  endif

else
  add_project_arguments(
    '-DUNIX',
  language : 'c')
endif

src=files([
  'src/afixcmd.c',
  'src/afixcmn.c',
  'src/arealist.c',
  'src/areatree.c',
  'src/cfg.c',
  'src/common.c',
  'src/fidoconf.c',
  'src/findtok.c',
  'src/grptree.c',
  'src/line.c',
  'src/stat.c',
  'src/version.c'
])

headers = files([
  'fidoconf/afixcmd.h',
  'fidoconf/arealist.h',
  'fidoconf/areatree.h',
  'fidoconf/common.h',
  'fidoconf/fc2tor_g.h',
  'fidoconf/fecfg146.h',
  'fidoconf/fidoconf.h',
  'fidoconf/findtok.h',
  'fidoconf/grptree.h',
  'fidoconf/stat.h',
  'fidoconf/tokens.h',
  'fidoconf/version.h'
])

incdir = include_directories('fidoconf')
smapi_proj = subproject('smapi')
smapi_dep=smapi_proj.get_variable('smapi_dep')

libfidoconf = library('fidoconfig', src,
  include_directories : incdir,
  dependencies:[smapi_dep],
  version:'1.9.0',
  install : true)

fidoconf_dep = declare_dependency(
  link_with: libfidoconf,
  dependencies: [smapi_dep],
  include_directories : incdir)

install_headers(headers, subdir: 'fidoconf')
