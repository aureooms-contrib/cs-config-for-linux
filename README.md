# Configuration
Configuration instructions for Linux @ ULB

- [Configuration](#configuration)
  * [Wireless connection (wifi)](#wireless-connection-wifi)
    + [Eduroam](#eduroam)
    + [Waffle](#waffle)
    + [\_TRUMP](#_trump)
  * [Wired connection (ethernet)](#wired-connection-ethernet)
  * [Printers](#printers)
    + [Troubleshooting](#troubleshooting)
  * [Allowed ports](#allowed-ports)

## Wireless connection (wifi)

### Eduroam
See https://github.com/aureooms/eduroam.

### Waffle
Ask Stefan for password. Needs authentication, see [instructions for wired connections](https://github.com/ulb/cs-config-for-linux/blob/master/README.md#wired-connection-ethernet).

### \_TRUMP
Ask Aurélien for password.

## Wired connection (ethernet)

Ethernet is authenticated using your NetID and password. You can login by going to [https://webauth.ulb.ac.be](https://webauth.ulb.ac.be) when plugged into the network. You can install [this script that automatically connects you to the network](https://github.com/aureooms-ulb/ulb). For example

    ulb auth once
    
> :warning: You should add the line `options single-request` at the top of `/etc/resolv.conf.head` and `/etc/resolv.conf` otherwise lots of request will timeout. The root cause is most likely due to bad network nodes configuration.

## Printers

> :warning: Printing only works with wired connection (ethernet) or `Waffle` or `_TRUMP` wifi but not with `eduroam` or `Plaine-Wifi`.

You need an account to use the printers. Ask the secretaries for an account if you do not have one. Try to login with your credentials on the [print server](https://fscd-printserver.ulb.ac.be:9192/user).

**If you cannot login to the print server, the first thing to do is to do the procedure of *changing* your password.
Go to https://idsapp.ulb.ac.be/pam, login and then go to https://idsapp.ulb.ac.be/pam/pammodpw.php. You must tick all the checkboxes (NetID, hydra, etc.), enter your username (NetID), your password, and submit the form. You do not really have to change your password: you can fill the input fields with your existing password. Once this is done, wait for 30 minutes then try to login to the [print server](https://fscd-printserver.ulb.ac.be:9192/user) again. If it still does not work, email the [SIS (Science Information Technology Support)](mailto:sis@ulb.ac.be).**

Install cups client. For example

    pacman -S cups

Add a ServerName entry pointing to the local cups server to `/etc/cups/client.conf`. For example

    # see 'man client.conf'
    # ServerName /run/cups/cups.sock #  alternative: ServerName hostname-or-ip-address[:port] of a remote server
    ServerName localhost    

Enable the cups-browsed service if you do not want to start it manually every time

    systemctl enable cups-browsed.service
    
And start it immediately if you want to print before the next reboot

    systemctl start cups-browsed.service

Follow (French) instructions at the bottom of [this page](http://sis.ulb.ac.be/dokuwiki/doku.php?id=ppcfsc). __TL;DR__: download [this directory](https://github.com/aureooms/dotfiles/tree/master/opt/papercut) and run the shell script that is inside as a daemon. An easy way to download the directory

    svn export https://github.com/aureooms/dotfiles/trunk/.opt/papercut
    
> :warning: `papercut` requires `java`. Java version 1.8 is recommended.
    
The printers network names are `DI-COPIER` and `DI-COLOR`:

  - use `DI-COLOR` only when you want to print colors,
  - use `DI-COPIER` otherwise.
  
> :warning: It can happen that those are listed multiple times because other users on the network decided to share those printers. In that case, look for names ending with `lit-printserver`.
  
`DI-COPIER` is also a scanner and a copier. The copying function requires a password which you can get from the secretaries. Here is [a reference sheet for the copier](https://ipfs.io/ipfs/QmNVBjifKRUR5AG3b5oDNgtnDe4uFLJ27Xo9PhkB7dU1bR).

### Troubleshooting

  - Again, printing only works with wired connection (ethernet) or `Waffle` or `_TRUMP` wifi but not with `eduroam` or `Plaine-Wifi`.
  - Make sure to set the paper size to A4 when printing. US letter will not work.
  - When you arrive at ULB, you will receive a temporary account which __can__ be used for printing. This account really is temporary and will stop working after you get your (definitive) account. Accounts user name ending with a digit are temporary.
    
## Allowed ports

    nmap -Pn $yourpublicip
    ...
    22/tcp   ssh
    873/tcp  rsync
    3389/tcp ms-wbt-server
    5800/tcp vnc-http
    5900/tcp vnc
