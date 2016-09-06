Dockerfile + several scripts
to run [FidoIP suite](https://sourceforge.net/projects/fidoip/)
with [Docker](https://www.docker.com/)

# Foreword

FidoIP has a lot of legacy irregularities like generating shell scripts
with hardcoded configuration to `/usr/local/bin`. So it is difficult a bit
to keep it in the box, but this Dockerfile tries to do it. Anyway we should
remember here that all this legacy stuff comes from DOS and OS/2, so it is
very nice itself that it can be deployed in Unix-like environment.

# Point mode

## To create configuration

1. `$ ./fido-docker-build`
2. `$ ./fido-init` and then inside container root shell (which will open):
    2.1. `# cd fidoip-1.0.5`
    2.2. `# setup_config.bash` and answer some questions
    2.3. `# ./set_perm.sh fido`

This will hopefully be simplified in the future.

After this, you will have your configuration in `usr` and `home` subfolders of current folder.
You can make changes to them from outside when container is not running.
For example, you can add `export TERM=xterm` or `export TERM=rxvt-unicode`
to `home/fido/.bashrc` and so on. BTW correct terminal line in `$TERM` is very
important for GoldEd to function properly.

`usr` and `home` subfolders contain your mail and settings,
so they are likely subject of backup if you practice it =).

## To use configuration

Run `$ ./fido`, then you will see container user shell

* `$ rs` to try to send/receive mail
* `$ g` to launch GoldEd

# Node mode

Have no experience in running full-featured nodes, so it is empty here
