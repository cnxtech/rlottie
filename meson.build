project('rlottie library',
        'cpp',
        license : 'Apache')

rlottie_lib_version = '0.0.1'

add_global_arguments('-DDEMO_DIR="@0@/example/resource/"'.format(meson.current_source_dir()), language : 'cpp')

compiler_flags = ['-Wall', '-O2', '-std=c++14', '-fvisibility=hidden']

if get_option('asan') == true
    compiler_flags += ['-fsanitize=address']
    add_global_link_arguments('-fsanitize=address', language: 'cpp')
endif

if get_option('msan') == true
    compiler_flags += ['-fsanitize=memory']
    add_global_link_arguments('-fsanitize=memory', language: 'cpp')
endif

if get_option('tsan') == true
    compiler_flags += ['-fsanitize=thread']
    add_global_link_arguments('-fsanitize=thread', language: 'cpp')
endif


if (build_machine.system() == 'linux')
    compiler_flags += ['-pthread']
    add_global_link_arguments('-pthread', language: 'cpp')
endif

add_global_arguments(compiler_flags, language: 'cpp')

inc = include_directories('inc')

subdir('inc')
subdir('src')

if get_option('example') == true
    subdir('example')
endif

if get_option('test') == true
   subdir('test')
endif

pkg_mod = import('pkgconfig')

pkg_mod.generate( libraries   : rlottie_lib,
                  version     : rlottie_lib_version,
                  name        : 'librlottie',
                  filebase    : 'rlottie',
                  description : 'A Library for rendering lottie files.'
                )
