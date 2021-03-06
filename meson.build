project('bag_rdr', 'cpp', default_options: ['cpp_std=c++11'])
add_project_arguments(['-Wno-maybe-uninitialized'], language : 'cpp')

deps = []
deps += dependency('liblz4')

common_cxx = declare_dependency(include_directories : include_directories('deps/common_cxx'))
deps += common_cxx

includes = []

extra_args = ['-DBAG_RDR_NO_ROS=1', '-DBAG_RDR_USE_SYSTEM_LZ4=1']
extra_args += get_option('extra_opt_flags')
if get_option('disable_bz2')
  extra_args += '-DDISABLE_BZ2'
else
  deps += declare_dependency(link_with : library('bz2'))
endif

sources = ['bag_rdr.cpp']
lib = static_library('bag_rdr', sources, cpp_args: extra_args, dependencies: deps, install: true)
install_headers('bag_rdr.hpp')
install_subdir('deps/common_cxx', install_dir : 'include')

pkg = import('pkgconfig')
libs = deps
h = includes
pkg.generate(lib,
             version : '0.1',
             name : 'bag_rdr',
             filebase : 'bag_rdr',
             description : 'A fast ROS bag reading library.',
             subdirs: ['.', 'common_cxx'],
             extra_cflags : extra_args)
