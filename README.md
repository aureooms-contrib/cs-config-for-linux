# config
Configuration instructions for Linux @ ULB

## Wifi

### Eduroam
See https://github.com/aureooms/eduroam.

### Waffle
Ask Stefan for password.

## Printers
:bangbang: Only works with wired (ethernet) connection.

:bangbang: Make sure to set the paper size to A4 when printing. US letter will not work.

Install cups client. For example

    pacman -S cups

Add a ServerName entry pointing to the local cups server to /etc/cups/client.conf. For example

    # see 'man client.conf'
    # ServerName /run/cups/cups.sock #  alternative: ServerName hostname-or-ip-address[:port] of a remote server
    ServerName localhost    

Enable the cups-browsed service if you do not want to start it manually every time

    systemctl enable cups-browsed.service
    
And start it immediately if you want to print before the next reboot

    systemctl start cups-browsed.service

Follow (French) instructions at the bottom of [this page](http://sis.ulb.ac.be/dokuwiki/doku.php?id=ppcfsc). Basically download [this directory](https://github.com/aureooms/dotfiles/tree/master/opt/papercut) and run the shell script that is inside as a daemon. An easy way to download the directory

    svn export https://github.com/aureooms/dotfiles/trunk/.opt/papercut
    
## Allowed ports

    22/tcp   ssh
    873/tcp  rsync
    3389/tcp ms-wbt-server
    5800/tcp vnc-http
    5900/tcp vnc
