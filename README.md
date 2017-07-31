# boss-docker-gnome-pygobject-gtk3-gst-cmusphinx-jhbuild

Gnome x Jhbuild x PyGObject x Cmusphinx x Gtk+3 in 🐳


[![Build History](https://buildstats.info/travisci/chart/bossjones/boss-docker-jhbuild-pygobject3)](https://travis-ci.org/bossjones/boss-docker-jhbuild-pygobject3)

[![Build Status](https://travis-ci.org/bossjones/boss-docker-jhbuild-pygobject3.svg?branch=master)](https://travis-ci.org/bossjones/boss-docker-jhbuild-pygobject3)
[![GitHub release](https://img.shields.io/github/release/bossjones/boss-docker-jhbuild-pygobject3.svg)]()
[![Docker Stars](https://img.shields.io/docker/stars/bossjones/boss-docker-jhbuild-pygobject3.svg)](https://hub.docker.com/r/bossjones/boss-docker-jhbuild-pygobject3/)
[![Docker Pulls](https://img.shields.io/docker/pulls/bossjones/boss-docker-jhbuild-pygobject3.svg)](https://hub.docker.com/r/bossjones/boss-docker-jhbuild-pygobject3/)
[![Contribution Guidelines](http://img.shields.io/badge/CONTRIBUTING-Guidelines-blue.svg)](./CONTRIBUTING.md)
[![LICENSE](https://img.shields.io/badge/license-Apache-blue.svg?style=flat-square)](./LICENSE)


# Jhbuild PyGObject3 Docker Image ([Dockerfile](https://github.com/bossjones/boss-docker-jhbuild-pygobject3))
[![](https://images.microbadger.com/badges/image/bossjones/boss-docker-jhbuild-pygobject3.svg)](https://microbadger.com/images/bossjones/boss-docker-jhbuild-pygobject3 "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/bossjones/boss-docker-jhbuild-pygobject3.svg)](https://microbadger.com/images/bossjones/boss-docker-jhbuild-pygobject3 "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/bossjones/boss-docker-jhbuild-pygobject3.svg)](https://microbadger.com/images/bossjones/boss-docker-jhbuild-pygobject3 "Get your own commit badge on microbadger.com")
[![](https://images.microbadger.com/badges/license/bossjones/boss-docker-jhbuild-pygobject3.svg)](https://microbadger.com/images/bossjones/boss-docker-jhbuild-pygobject3 "Get your own license badge on microbadger.com")

NOTE: This is a prereq for `scarlett_os`. It makes some strong assumptions about how you plan on running jhbuild, and should mainly just run on CI systems.

Docker container that installs an jhbuild environment that has the following:

1. Python3
2. Jhbuild
3. Glib
4. Gobject-introspection
5. Gstreamer
6. Gst-Espeak-Plugin
7. Gtk3
8. Pocketsphinx/Sphinxbase


Compiling jhbuild and deps ( Prerequisites )
-------------

Building from tarball requires:

 - gcc or clang (_for compiling_)
 - libxft (_for font rendering_)
 - libxinerama (_for XINERAMA support_)
 - gdk-pixbuf2 (_for pixmap rendering_)
 - libxrandr (_for XRANDR support_)
 - libsndfile (_for sound support_)
 - libsm (_for X11R6 session management_)
 - fribidi (_for i18n text rendering_)

Building from git also requires:

 - git (_for cloning the git repository and updating changelogs_)
 - autoconf/automake or cmake toolchain (_for build scripts_)
 - xorg-mkfontdir (_for installing themes_)
 - asciidoctor or asciidoc (_for creating html documentation_)
 - markdown (_for building release package_)



# Build

`docker build -t docker-gnome-pygobject-gtk3-gst-cmusphinx-jhbuild .`

# Links

- https://github.com/search?q=execlineb+sshd&type=Code&utf8=%E2%9C%93


# Order of operations

```
jhbuild_pygobject3_1  | [init] no run.d scripts
jhbuild_pygobject3_1  | [run] starting process manager
jhbuild_pygobject3_1  | [s6-init] making user provided files available at /var/run/s6/etc...exited 0.
jhbuild_pygobject3_1  | [s6-init] ensuring user provided files have correct perms...exited 0.
jhbuild_pygobject3_1  | [fix-attrs.d] applying ownership & permissions fixes...
jhbuild_pygobject3_1  | [fix-attrs.d] done.
jhbuild_pygobject3_1  | [cont-init.d] executing container initialization scripts...
jhbuild_pygobject3_1  | [cont-init.d] 00-init-ssh: executing...
jhbuild_pygobject3_1  | [cont-init.d] 00-init-ssh: exited 0.
jhbuild_pygobject3_1  | [cont-init.d] done.
jhbuild_pygobject3_1  | [services.d] starting services
jhbuild_pygobject3_1  | [services.d] done.
```

# Environment Variables

Variable | Example | Description
--- | --- | ---
`S6_KILL_FINISH_MAXTIME` | `S6_KILL_FINISH_MAXTIME=1` | Wait time (in ms) for zombie reaping before sending a kill signal
`S6_KILL_GRACETIME` | `S6_KILL_GRACETIME=1` | Wait time (in ms) for S6 finish scripts before sending kill signal
`SERVER_LOG_MINIMAL` | `SERVER_LOG_MINIMAL=1` | Wait time (in ms) for S6 finish scripts before sending kill signal
`SERVER_APP_NAME` | `SERVER_APP_NAME=jhbuild-compile` | Set application name for stdout logging info
`COMPOSE_PROJECT_NAME` | `COMPOSE_PROJECT_NAME=jhbuild-compile` | The default project name is the basename of the project directory. You can set a custom project name by using the -p command line option or the this environment variable.
`SCARLETT_ENABLE_SSHD` | `SCARLETT_ENABLE_SSHD=1` | When set to 0, openssh-server will be enabled for development use w/ VSCode or Sublime
`SCARLETT_ENABLE_DBUS` | `SCARLETT_ENABLE_DBUS='true'` | When set, a session dbus service will be started
`SCARLETT_BUILD_GNOME` | `SCARLETT_BUILD_GNOME='true'` | When set, jhbuild and deps will be compiled
`TRAVIS_CI` | `TRAVIS_CI='true'` | Signal s6 to stop when finished all run.d scripts. Important for CI builds.

* `with-contenv` tool, which is used to expose environment variables across scripts, has a limitation that it cannot read beyond 4k characters for environment variable values. To work around this issue, use the script `/scripts/with-bigcontenv` instead of `with-contenv`. You'll need to remove the `with-contenv` from the shebang line, and add  `source /scripts/with-bigcontenv` in the next line after the shebang line.

### Startup/Runtime Modification

To inject changes just before runtime, shell scripts may be placed into the
`/etc/cont-init.d` folder.
As part of the process manager, these scripts are run in advance of the supervised processes. @see https://github.com/just-containers/s6-overlay#executing-initialization-andor-finalization-tasks


# Optional Arguments

Variable | Example | Description
--- | --- | ---
`SCARLETT_ENABLE_SSHD` | `SCARLETT_ENABLE_SSHD=0` | When set to 0, openssh-server will be enabled for development use w/ VSCode or Sublime
`SCARLETT_ENABLE_DBUS` | `SCARLETT_ENABLE_DBUS='true'` | When set, a session dbus service will be started
`SCARLETT_BUILD_GNOME` | `SCARLETT_BUILD_GNOME='true'` | When set, jhbuild and deps will be compiled
`TRAVIS_CI` | `TRAVIS_CI='true'` | Signal s6 to stop when finished all run.d scripts. Important for CI builds.

```
