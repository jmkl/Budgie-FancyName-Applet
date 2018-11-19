project('budgie-fancyname-applet',
	version: '0.1.0',
	meson_version: '>= 0.40.0'
)

i18n = import('i18n')
python = import('python3')
gnome = import('gnome')

message('Looking for dependencies')
python_bin = python.find_python()
if not python_bin.found()
	error('No python3 binary found')
else
	message('Found python3 binary')
endif
dependency('glib-2.0')
dependency('budgie-1.0', version: '>=2')
dependency('gobject-introspection-1.0', version: '>=1.51.1')
dependency('gtk+-3.0', version :'>=3.22')

# Global path variabel
prefix = get_option('prefix')
libdir = join_paths(prefix, get_option('libdir'))
datadir = join_paths(prefix, get_option('datadir'))
ICON_INSTALL_DIR = join_paths(datadir, 'icons', 'hicolor')
APPLET_INSTALL_DIR = join_paths(libdir, 'budgie-desktop',
	'plugins', meson.project_name())

conf = configuration_data()
conf.set('PROJECT_NAME', meson.project_name())

message('Installing applet...')

install_data(
    'MyFancyApplet.plugin',
    install_dir: APPLET_INSTALL_DIR
)
install_data(
    'com.solus.budgie-fancyname.gschema.xml',
    install_dir: join_paths(datadir, 'glib-2.0', 'schemas'),
)

meson.add_install_script('post-install')

configure_file(
	input: 'MyFancyApplet.py.in',
	output: 'MyFancyApplet.py',
	configuration: conf,
	install_dir: APPLET_INSTALL_DIR
)
