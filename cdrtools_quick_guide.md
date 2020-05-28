![British Library Logo](./assets/BL_Logo_RGB_100pixels_high.jpg)
# Save our Sounds – Unlocking our Sound Heritage
 ### cdrtools Quick Start Guide
_April 22nd 2020_
Tom Ruane
tom.ruane@bl.uk

cdrtools is an open source, unix based suite of cd reading/writing tools developed by Jörg Schilling -  [http://cdrtools.sourceforge.net/private/cdrecord.html](http://cdrtools.sourceforge.net/private/cdrecord.html)

The quickest way to install cdrtools is via homebrew: `brew install cdrtools`

It can also be compiled from sourceforge -  [https://sourceforge.net/projects/cdrtools/](https://sourceforge.net/projects/cdrtools/)

Before you can run any commands you need to prevent the optical drive from mounting the disc, before doing anything else run the following command in the terminal:

    sudo kill -STOP  `(ps -ef | grep diskarbitrationd | awk '{ print $2 }')`

To remount the drive when you’re finished and want to properly eject the disc, run:

    `sudo kill -CONT  `(ps -ef | grep diskarbitrationd | awk '{ print $2 }')

To find your optical drive number so you can run commands on the relevant device, run -scanbus:

    cdrecord -scanbus
    
    1,0,0 100) 'MATSHITA' 'DVD-R UJ-898 ' 'HC10' Removable CD-ROM

My optical drive number is 1,0,0.

You can now insert a compact disc and run a variety of tools, for example:

View the TOC `cdrecord -toc dev=1,0,0`

Read the ATIP `cdrecord -atip dev=1,0,0`

A full list of the tools included with cdrtools and the commands for each can be found here:  [http://cdrtools.sourceforge.net/private/man/cdrecord/](http://cdrtools.sourceforge.net/private/man/cdrecord/)
