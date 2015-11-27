# config
Configuration instructions for Linux @ ULB

## Wifi

### Eduroam
See https://github.com/aureooms/eduroam.

### Waffle
Ask Stefan for password.

## Printers
/!\ Only works with wired (ethernet) connection.
Install cups client. For example

    pacman -S cups

Add a ServerName entry pointing to `lit-printserver.ulb.ac.be:631` to /etc/cups/client.conf. For example

    # see 'man client.conf'
    ServerName /run/cups/cups.sock #  alternative: ServerName hostname-or-ip-address[:port] of a remote server
    ServerName lit-printserver.ulb.ac.be:631
    
Follow (French) instructions at the bottom of [this page](http://sis.ulb.ac.be/dokuwiki/doku.php?id=ppcfsc). Basically download [this directory](https://github.com/aureooms/dotfiles/tree/master/opt/papercut) and run the shell script that is inside as a daemon. An easy way to download the directory

    svn export https://github.com/aureooms/dotfiles/trunk/opt/papercut
