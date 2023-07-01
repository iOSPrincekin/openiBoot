#
# Setup our cross-compilation environment.
#

import os

def ARMEnvironment(*a, **kw):
	env = Environment(tools=['gas', 'gcc', 'gnulink', 'ar'], ENV=os.environ, *a, **kw)
	plat_flags = ['-mlittle-endian', '-mfpu=vfp', '-mthumb', '-mthumb-interwork', '-fPIC', '-Wno-error=unused-but-set-variable', '-fno-strict-aliasing', '-Wno-error=maybe-uninitialized']
	env.Append(CPPPATH = ['#includes'])
	env.Append(CPPFLAGS = plat_flags+['-nostdlib'])
	env.Append(ASPPFLAGS = ['-xassembler-with-cpp'])
	env.Append(LINKFLAGS = plat_flags+['-nostdlib', '-Ttext=0x0', '-L./'])
	env.Append(LIBS = ['gcc'])

	env['PROGSUFFIX'] = ''

	if not "CROSS" in env:
		if "CROSS" in env['ENV']:
			env['CROSS'] = env['ENV']['CROSS']
		else:
			env["CROSS"] = 'arm-elf-'

	env["CC"] = env["CROSS"] + 'gcc-4.7'
	env["OBJCOPY"] = env["CROSS"] + 'objcopy'
	env["AR"] = env["CROSS"] + 'ar-4.7'
	#env["LINK"] = 'arm-none-eabi-ld'
	return env
Export('ARMEnvironment')