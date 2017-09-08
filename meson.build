project('Vibe-DB-PostgreSQL', 'd',
    meson_version: '>=0.40',
    license: 'MIT',
    version: '0.3.0'
)

project_soversion = '0'

#
# Dependencies
#
pkgc = import('pkgconfig')
dpq2_dep = dependency('dpq2', version: '>= 0.6.24', fallback: ['dpq2', 'dpq2_dep'])
vibe_core_dep = dependency('vibe-core', version: '>= 0.8')

#
# Sources
#
vibe_db_postgresql_src = [
    'source/vibe/db/postgresql/test.d',
    'source/vibe/db/postgresql/package.d'
]

src_dir = include_directories('source/')

#
# Targets
#
vibe_db_postgresql_lib = library('vibe-postgresql',
        [vibe_db_postgresql_src],
        include_directories: [src_dir],
        dependencies: [dpq2_dep, vibe_core_dep],
        install: true,
        version: meson.project_version(),
        soversion: project_soversion
)
pkgc.generate(name: 'vibe-postgresql',
              libraries: vibe_db_postgresql_lib,
              subdirs: 'd/vibe',
              version: meson.project_version(),
              requires: ['dpq2', 'vibe-core'],
              description: 'PostgreSQL support for Vibe.d'
)

# to allow others to easily use this as a subproject
vibe_postgresql_dep = declare_dependency(
    link_with: [vibe_db_postgresql_lib],
    include_directories: [src_dir],
    dependencies: [dpq2_dep, vibe_core_dep]
)

#
# Install
#
install_subdir('source/vibe/', install_dir: 'include/d/vibe/')
