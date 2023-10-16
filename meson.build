project('objc-boilerplate', 'objc', version : '0.1.0')

# Ensure clang is used for Objective-C
objc_compiler = meson.get_compiler('objc')
if objc_compiler.get_id() != 'clang'
  error('Clang is required for this project. Please set CC=clang, and OBJC=clang before running Meson.')
endif

# Objective-C (GNUstep) support from gnustep-config
gnustep_config = find_program('gnustep-config', required: true)
if not gnustep_config.found()
    error('GNUstep is required for this project. Please install GNUstep and ensure gnustep-config is in your PATH. You might want to source GNUstep.sh before running Meson.')
endif

gnustep_flags = run_command(gnustep_config, '--objc-flags', check: true).stdout().strip().split()
gnustep_base_libs = run_command(gnustep_config, '--base-libs', check: true).stdout().strip().split()

# Filter out flags that are handled by Meson's built-in options
filtered_objc_flags = []
foreach flag : gnustep_flags
if flag != '-Wall' and flag != '-g' and flag != '-O2'
    filtered_objc_flags += flag
endif
endforeach

# Enable ARC (Automatic Reference Counting)
filtered_objc_flags += '-fobjc-arc'

# Add Objective-C flags and libraries
add_project_arguments(filtered_objc_flags, language: 'objc')
add_project_link_arguments(gnustep_base_libs, language: 'objc')

source = [
    # Objc files
    'src/main.m',
]

executable('objc-boilerplate', source)