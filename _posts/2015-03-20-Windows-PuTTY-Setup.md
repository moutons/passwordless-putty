---
layout: post
title: Windows PuTTY Setup
---
# The Scoop
This is a straightforward step-by-step guide to getting the PuTTY SSH client set up so you can log into your Linux server\* from your Windows workstation. You can read all about [Public Key Cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography), [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell), and other related topics on an internet near you.

*\*or other system running OpenSSH*

# Getting PuTTY

![getting PuTTY](https://i.imgur.com/ZCbC1Am.png)

The download's [been here for ages](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html). Get the one marked "A Windows installer for everything except PuTTYtel".

# Installer

![Installer](https://i.imgur.com/l10Ci1b.png)

There are a few other setup screens, but make sure the "Associate .PPK files (PuTTY Private Key) with Pageant and PuTTYgen" option is checked, on the "Select Additional Tasks" screen. Everything else can probably be left at defaults\*

*\* this option is also a default option as of putty-0.63*

# PuTTY folder in the start menu

![PuTTY folder in the start menu](https://i.imgur.com/v6JvMsA.png) 

The programs we'll be using here are PuTTYgen (to generate the key pair), Pageant (SSH key agent, advanced topic), and PuTTY itself.

Open PuTTYgen.

![PuTTYgen](https://i.imgur.com/dexPWVl.png) 

Here's what the main PuTTYgen screen looks like. We'll be generating a 2048-bit SSH-2 RSA keypair, which is compatible with most OpenSSH servers running as of 2015-01-26.

# PuTTYgen Parameters

![PuTTYgen Parameters](https://i.imgur.com/jllGg9y.png)

You can see in the Parameters area that the Type of key is SSH-2 RSA, and the number of bits is 2048.

# Click Generate

![Click Generate](https://i.imgur.com/z3h7uLq.png)

In the Actions area!

# Screen Change Now

![Screen Change Now](https://i.imgur.com/IrpWIqw.png)

The Key area of the app will change, with this green progress bar indicating that randomness is being generated. 

# Oooooh, random!

![Oooooh, random!](https://i.imgur.com/l17vRbz.png)

Wiggle the mouse around in the application window until the thing's done doing whatever it does. As long as the green bar is moving towards the right of the screen you should be okay, although I don't have advice on what to do if it's not.

# Job's done!

![Job's Done!](https://i.imgur.com/EYInC4Q.png)

Once the randomness is generated PuTTYgen will do some maths and spit out your keypair. When the app looks something like this your keypair has been generated.

# Save Private Key

![Save Private Key](https://i.imgur.com/PMHukX3.png)

It's time to save the private key.

# Hey, no passphrase

![Hey, no passphrase](https://i.imgur.com/Ltf0A4r.png)

This will only show up if you don't set a passphrase. If you type a passphrase in the "Key Passphrase" and "Confirm Passphrase" sections before saving, your key will be protected better against unauthorized use. 

It's a good idea to do this, and Pageant will help you from having to type in the passphrase all the time if it's set up right.

I didn't do it, specifically in order to generate this warning.

# Where do you want to save the file?

![Where do you want to save the file?](https://i.imgur.com/yiwY3EZ.png)

Browse in the familiar Windows File dialog to a location where you want to save the SSH Key files. Here I have selected the root of the C: drive, which is a fairly poor location. I recommend protecting the private key with a strong passphrase, and saving it somewhere safe and securely backed up.

Or on Dropbox, they're probably trustworthy.

# Select the "Public key for pasting into OpenSSH authorized_keys file" text

![Select the "Public key for pasting into OpenSSH authorized_keys file" text](https://i.imgur.com/R0X4fyh.png)

Right-click inside this area, choose "Select All", and Ctrl-V or right-click again and choose "Copy".

Save this into a file with the extension .txt somewhere appropriate, like your desktop or Google Drive (I'm being totally serious this time).

Share this key with anyone who wants to authorize you to connect to their system. There's a reason this portion of the keypair is called the "Public Key".

**The next five steps are optional, read [about the Pageant agent](https://the.earth.li/~sgtatham/putty/0.58/htmldoc/Chapter9.html) to find out what it does**


# Optional - Now open Pageant

![Now open Pageant](https://i.imgur.com/TzMK4Yj.png)

When you open Pageant from the start menu, it will probably minimize to the Windows System Tray. Youve got to right-click the icon to get a Pageant menu. Mine hid after a second or two, so you'll then have to click the disclosure triangle to see the icon in the hidden portion of the System Tray.

# Optional - Pageant Menu

![Pageant Menu](https://i.imgur.com/iOnmI8h.png)

View Keys is the option you want\*

*\*although once you've got things all set up you can connect directly to a server by choosing an option from "Saved Sessions" here.*

# Optional - Pageant's default application window

![Pageant's default application window](https://i.imgur.com/uPnLxhb.png)

You'll want to Add Key here, so the Pageant SSH agent will know to try to use the SSH private key to set up the SSH session. You can have multiple keys in Pageant, and it'll most likely set up the connection using the appropriate keypair, but you don't have to worry about that now.

# Optional - Choose the Private key from wherever you saved it

![Choose the Private key from wherever you saved it](https://i.imgur.com/4mllGhg.png)

The Pageant Add Key dialog will only display Folders and PPK keys by default, which is what you want. Browse to the location you saved the file and select it.

If you set up a passphrase to protect the key Pageant will prompt you to enter it here to decrypt the key.

# Optional - Key's been added

![Key's been added](https://i.imgur.com/QkrH509.png)

This is what Pageant looks like once your key's been loaded.

# Now to PuTTY to set up the Session

![setting up your session](https://i.imgur.com/l10Ci1b.png)

PuTTY has a ton of options, and we'll try to keep it simple. I usually save a session first, so I have sort of a placeholder session that I can load whenever I am making a connection to a new machine using a previous keypair.

# Saving placeholder session

![Saving placeholder session](https://i.imgur.com/M1uMmNR.png)

Enter 127.0.0.1 in the "Host Name (or IP address) field, and in the "Saved Sessions" field, then click Save.

You'll now see it in the list under the "Saved Sessions" field, and you can overwrite it with your default settings whenever they change.

# SSH Auth options

![SSH Auth options](https://i.imgur.com/Okuvo83.png)

Click the disclosure button next to the "SSH" Category on the left of the screen, so you can select "Auth". Here, **if you didn't set up Pageant, you can select the particular SSH Private Key to use for a connection**.

# Optional - Auth private key

![Auth private key](https://i.imgur.com/HZTlL1V.png)

If you need to, browse to the appropriate PPK file and select it here.

# Optional - Auth private key selected

![Auth private key selected](https://i.imgur.com/wKg7Lfa.png)

This is what it will look like if you've selected a private key. Remember, Pageant can do this for you if you don't mind having the SSH Key Agent running in the background.

# Optional - Specify Username

![Specify Username](https://i.imgur.com/0IvdHpo.png)

Here you can specify a username to send to the server when you are attempting to connect, and what to do if the username is not specified.

The default option, "Prompt", is a good option.

# Putting it all together

![Putting it all together](https://i.imgur.com/9bhvNj4.png)

I have gone back to the main "Category" from the left-hand menus, "Sessions", and saved the 127.0.0.1 Session Profile. Now, I get the IP address of the machine I want to connect to, and enter it in the "Host Name" and "Saved Sessions" field and click "save".

This only matters if you want these session settings to be available later. If DNS is set up properly, you can substitute the hostname for the IP address here, and PuTTY will perform a DNS lookup when trying to connect.

# First time's the charm

![First time's the charm](https://i.imgur.com/Mhu3Vx6.png)

When connecting to a SSH server you haven't connected to before, you'll be prompted to acknowledge the server's host key. The topic of host keys is a little outside the scope of this guide, and in most circumstances you can blissfully acknowledge the key.

If the server is replaced by another using the same IP address or hostname, you may see another prompt in the future. Proceed carefully through, reading each dialog in that case, asking for help if necessary.

# PuTTY prompts for username

![PuTTY prompts for username](https://i.imgur.com/uGWu9s9.png)

I did not select a username to send by default for this connection, so PuTTY prompts me for the username I would like to attempt to connect using.

# Connection continues

![Connection continues](https://i.imgur.com/iXhFFQA.png)

I select "root" since I have associated my newly generated SSH key with the "root" account, and hit Enter. Putty attempts to connect using "root" and the putty-rsa-2048.ppk private key I selected earlier to authenticate to this system, and succeeds.

# Now I show the authorized_keys file

![Now I show the authorized_keys file](https://i.imgur.com/2ec9bqT.png)

The command `cat ~/.ssh/authorized_keys` displays the contents of that file. In the future, if I have access to write to that file I can add additional SSH keys to authenticate to the "root" account, although it would be a far better idea to set up other user accounts and use `sudo` to give admin rights as appropriate.

# This is the end