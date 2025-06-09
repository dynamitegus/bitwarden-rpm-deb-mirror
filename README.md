# The Bitwarden RPM&Deb Mirror Repository

Original script by https://gitlab.com/paulcarroty/atom-rpm-deb-mirror/
Original Bitwarden script by https://github.com/SISheogorath/bitwarden-rpm-deb-mirror

> [!CAUTION]
> DO NOT USE THIS FOR PRODUCTION, not only am I not affiliated with Bitwarden or any of the above people, but this repo was originally a test repo modified by SISheogorath, **You should not be blindly trusting me or SISheogorath**, and I am not liable for any problems that arrive becuase of this, I just want a way to auto update my bitwarden client.

> [!IMPORTANT]
> I do not provide **any** garantee that I will fix any issue that get posted in github, unless it directly effects me. Go fix it yourself or submit your pull request.

Mirroring **the OFFICIAL Bitwarden packages for Linux** directly on GitHub. The update script code and TravisCI config & pipeline log is open source.

## How to install

#### The metadata of each repository is signed - for correct work you also need to add my GPG key:
* `rpm --import https://sisheogorath.github.io/bitwarden-rpm-deb-mirror/pub.gpg`
* `wget -qO - https://sisheogorath.github.io/bitwarden-rpm-deb-mirror/pub.gpg | sudo apt-key add -`

### Add the repository:
* **Debian/Ubuntu/Linux Mint**: `echo 'deb https://sisheogorath.github.io/bitwarden-rpm-deb-mirror/debs/ bitwarden main' >> /etc/apt/sources.list`

* **Fedora/RHEL**: `dnf config-manager --add-repo https://sisheogorath.github.io/bitwarden-rpm-deb-mirror/rpms/`

* **openSUSE/SUSE**: `zypper addrepo -t YUM https://sisheogorath.github.io/bitwarden-rpm-deb-mirror/rpms/ bitwarden_mirror_on_github`

### Then type `bitwarden` in [GNOME Software](https://wiki.gnome.org/Apps/Software) or use your package manager:

* `apt install bitwarden`
* `dnf install bitwarden`
* `zypper in bitwarden`


## How to create an own repository

Generate your keys like explained here:
https://www.digitalocean.com/community/tutorials/how-to-use-reprepro-for-a-secure-package-repository-on-ubuntu-14-04#prepare-and-publish-a-signing-key

Export them using `gpg --export-secret-subkeys --export-options export-reset-subkey-passwd <keymailaddress> > signing.key`

Encrypt them using `openssl enc -aes-256-cbc -salt -a -in signing.key -out signing.key.enc -k <yourpassword>`

Add `$KEY` to your travis settings so it can be decrypted online.
