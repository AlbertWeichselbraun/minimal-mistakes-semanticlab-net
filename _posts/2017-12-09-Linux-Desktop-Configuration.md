--- 
title: Linux Desktop Configuration
layout: single
categories: Linux
--- 

This post provides suggestions for a suitable linux desktop configuration

### Gnome3 Desktop

 1. Limit `Alt`+`Tab` to current workspace: 
  
    ```bash
    gsettings set org.gnome.shell.app-switcher current-workspace-only true
    ```

### E-Mail

I use Thunderbird in conjunction with the following addons:

 1. Lightning (Calendar)
 2. Calendar tweaks
 3. CardBook (CardDAV support)
 4. Enigmail (PGP support)
 5. Nostalgy (efficient, keyboard based navigation)
 6. Quicktext (template support)


### Advanced PDF editing

Unfortunately, libpoppler-based PDF editors such as evince, okular, etc. do not support all PDF features required for editing more complex forms. I, therfore, use [PDF-Xchange-Editor](https://www.tracker-software.com/product/pdf-xchange-editor) a powerful alternative that supports most relevant features in the free version.

 1. Download Editor Plus Portable Version and unpack it in `/opt` 
 2. Run the software with `wine`.

### Additional software

 1. KeepassXC password manager
    ```bash
    add-apt-repository ppa:phoerious/keepassxc
    ```
