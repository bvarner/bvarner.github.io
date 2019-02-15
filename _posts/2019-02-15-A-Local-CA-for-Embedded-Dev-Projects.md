Since the printer has been working for a year now, it's time to document some things I'm doing with it.

I've pushed quite a few things to my [bricabrac git repo](https://github.com/bvarner/bricabrac) where I stash my OpenSCAD sources for [my thingiverse designs](https://www.thingiverse.com/varnerrants/designs). I've also undertaken a few raspberrypi based projects, building embedded linux images with yocto and openembedded. I've found I like that approach. Far moreso than trying to maintain debian based iamges, and with the added benefit of being able to set the rootfs to be read-only.

So I'm printing cases and things that involve raspberrypi's with embedded images. Most of these images have a server software stack of some sort running on them. Which brings me to the topic today.

Being able to issue certificates for these embedded images, and have them trusted on my devices. The [Let's Encrypt page on the topic](https://letsencrypt.org/docs/certificates-for-localhost/) is a good read, and pointed me down this path. I'm documenting it here, for my own benefit in the future. (Hello, Future me.)

I looked into [caman](https://github.com/radiac/caman) which seems pretty nice and robust. It would work well, if I were trying to do this corporately, or was planning on putting these devices on public networks or in places they could get easily compromised. I'm not, so this seems a bit overly complex.

Next up is [minica](https://github.com/jsha/minica) which seems about right, and was referenced by the Let's Encrypt documentation. So why not.


1. On my debian workstation, I installed minica into a directory.
2. Made sure I had the `ca-certificates` package installed with `sudo apt-get install ca-certificates`
3. Copied the root CA pem as a crt to the proper directory: `sudo sudo mkdir -p /usr/share/ca-certificates/minica && sudo cp minica.pem /usr/share/ca-certificates/minica/minica.crt`
4. Made it rebuild the list of certs with `sudo dpkg-reconfigure ca-certificates`

And that should do it for most things... except for Chrome. Because it's stupid.

So I created a new nssdb....
```
mkdir -p $HOME/.pki/nssdb
certutil -d $HOME/.pki/nssdb -N
certutil -d $HOME/.pki/nssdb -L
```
Hey look, it's empty!

Then I imported the pem... and made sure it looked right.
```
certutil -d $HOME/.pki/nssdb -A -t "C,," -n "minica" -i minica.pem 
certutil -d $HOME/.pki/nssdb -L
certutil -L -d $HOME/.pki/nssdb -n "minica"
```

I think quit / restarted Chrome, was asked the passphrase for the new nssdb, and ... *BAM*
my "org-minica" root cert is listed as trusted. :-D