Dockerfile + several scripts
to run [FidoIP suite](https://sourceforge.net/projects/fidoip/)
with [Docker](https://www.docker.com/)

# Why?..

                      __
                     /  \
                    /|oo \
                   (_|  /_)
                    _`@/_ \    _
                   |     | \   \\
                   | (*) |  \   )) 
      ______       |__U__| /  \//
     / FIDO \       _//|| _\   /
    (________)     (_/(_|(____/

**Why FidoNet?** Because it is cool and still more than alive.

**Why Docker?** FidoIP has a lot of irregularities like generating shell scripts
with hardcoded configuration to `/usr/local/bin`. So it is difficult a bit
to keep it in the box, but this Dockerfile tries to do so. Anyway we should
remember here that all this charming oldschool stuff comes from DOS (it is quite ok
to store user data in system directory then =) ) and OS/2, so it is
very nice itself that it can be deployed in Unix-like environment.

**Why 32 bit?** Just because my server is x86 PC. You are free to derive it from 64 bit
image and use `fido_linux.64.sh` instead of `fido_linux.sh` to build this software.

# Point mode

## To create configuration

1. `$ ./fido-docker-build`
2. `$ ./fido-init` and then inside container root shell (which will open):
    1. `# cd fidoip-1.0.5`
    2. `# ./setup_config.bash` and answer some questions
    3. `# ./set_perm.sh fido`

This will hopefully be simplified in the future.

After this, you will have your configuration in `usr` and `home` subfolders of current folder.
You can make changes to them from outside when container is not running.
For example, you can add `export TERM=xterm` or `export TERM=rxvt-unicode`
to `home/fido/.bashrc` and so on. BTW correct terminal line in `$TERM` is very
important for GoldEd to function properly.

`usr` and `home` subfolders contain your mail and settings,
so they are likely subject of backup if you practice it =).

## To use configuration

Run `$ ./fido-shell`, then you will see container user shell

* `$ rs` to try to send/receive mail
* `$ g` to launch GoldEd

If you want to automate `$ rs`, `./fido-rs` is at your service, it just launches `rs` in `fido-shell`.

# Node mode

Have no experience in running full-featured nodes, so it is empty here
