project('usbrelay', 'c')

#WORK ON FREEBSD only!


# gen_gitversion_h = custom_target('generate-gitversion',
#   input: 'Makefile',
#   output: 'gitversion.h',
#   command: ['gmake', -f'@OUTPUT@'],
#   capture: false
# )

cc = meson.get_compiler('c')

run_command('sh', '-c', 'echo "#define GITVERSION \"42\"" > gitversion.h')

# need libusb-hidapi
hidapi_dep = dependency('hidapi', method : 'pkg-config', required : true)

hidapi_inc = include_directories('/usr/local/include/')

libusbrelay = static_library('libusbrelay',
    sources : ['libusbrelay.c'],
    include_directories : hidapi_inc,
    dependencies : [hidapi_dep])


#need to install argp-standalone
argp_lib = cc.find_library('argp', dirs: ['/usr/local/lib'], required: true)

executable('usbrelay',
    'usbrelay.c',
    link_with : libusbrelay,
    dependencies: [argp_lib],
    include_directories : hidapi_inc,
    )
