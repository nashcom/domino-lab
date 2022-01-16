# Install Domino 12.0.1 native on Linux

Yes, we are using Domino on Linux.
DON'T PANIC!
Count to 10, then panic!

Just kidding...

What if the whole setup is as easy as installing it on Windows?

Introducing: Nash!Com Domino on Linux One Touch Install  
(From zero to a running Domino server in 10 minutes)

Reference: https://github.com/IBM/domino-docker/blob/master/start_script/docs/install_domino.md

## Define where to download the software from

The script can either use software locallay or from a remote location:

```
export SOFTWARE_DIR=/local/software
export DOWNLOAD_FROM=https://myserver.com/software
```

Our lab has software downloaded to `/local/software` -- the default setting.

## On-the-fly run Domino install script directly from github.com

- Finds out about the latest Domino version and your Linux version
- Installs all the required Linux packages
- Setup for notes:notes user and system settings
- Installs start script

Usually it is not a good idea to run files directly downloaded from the internet.  
This is a download from our GitHub project validated by HTTPS and should be fine.

```
curl -sL https://github.com/IBM/domino-docker/raw/develop/start_script/install_domino.sh | bash -
```

## Configure your Domino server

```
domino setup auto
```

Finds out the prepared configuration for your domain.  
Downloads the configuration and prompts you for environment variables prepared for your server.

## Run your Domino server

```
domino start
```

## Live console

```
domino console
```

# Connect to your newly configured server via HTTPS

Just use machine's hostname and check the certificate, setup created for you.

# Connect to your server via NRPC

The most convenient way would be to use the Microsoft Virtual Sandbox.

It can be installed as an optional component running the following command:

```
optionalfeatures.exe
```

## Option A - Install Notes 12.0.1 Client in Windows Sandbox or VM

Launch the Windows sandbox or any other virtualization software and download the client.

- Notes Basic Client
- Notes Admin and Design Client

Export the download location.  
The URL is already set on your lab server accordingly

```
set LAB_DOWNLOAD=http://download.acme.com
```

```
curl -LO %LAB_DOWNLOAD%/Notes_12.0.1_Basic_Win_English.exe
curl -LO %LAB_DOWNLOAD%/Notes_Designer_Admin_12.0.1_Win_English.exe
```

Run the installer

## Option B - Copy preinstalled Notes 12.0.1 Basic Client

In case you don't have a Notes 12.0.1 client, download a pre installed client.  
To not conflict with any other client, it was installed in `c:\notesbasic1201`.  
But you can change the `notes.ini` to run it from a different path as well.

### Download software

```
curl -LO %LAB_DOWNLOAD%/notesbasic1201.zip
```

### Extract software

Open the zip via explorer and copy the files to c:\

# Setup Notes Client

Launch Notes Client and connect to your server.  
Your ID has been uploaded to ID Vault setup automatically with Domino 12 One-Touch setup.

Specify your first name and last name and the hostname of your server.  

# Download deSEC e.V. configuration

```
curl -LO https://raw.githubusercontent.com/HCL-TECH-SOFTWARE/domino-cert-manager/main/dns-providers/desec/certstore_desec.dxl
```
Import DXL file to certstore.nsf.


# Install nshcertool

We will use the tool later in the workshop.  It is available for Windows and Linux.

- For Linux it uses the already installed OpenSSL 1.1.1 Libs.
- For Windows you should copy it into your Notes client binary directory to use the Notes OpenSSL Libs.

## Windows

```
cd c:\notesbasic1201
curl -LO $LAB_DOWNLOAD/nshcertool.exe
```

## Linux

```
curl -L $LAB_DOWNLOAD/nshcertool -o /usr/bin/nshcertool
chmod +x /usr/bin/nshcertool
```

For each user copy the cacert.pem file

```
cp /local/notesdata/cacert.pem ~/nshcertool/cacert.pem
```

# Useful OpenSSL commands

## Show certificate information

```
openssl x509 -text -noout -in cert.pem
```

## Get certs from a remote host in PEM

```
echo | openssl s_client -servername blog.nashcom.de -showcerts -connect blog.nashcom.de:443
```

## Export certs from PEM to PKCS#12 (P12/PFX)

```
openssl pkcs12 -export -out certs.p12 -in certs.pem -password pass:mypassword
```

## Export certs from PKCS#12 (P12/PFX) to PEM

```
openssl pkcs12 -in certs.pfx -out certs.pem -nodes
```

## Convert PKCS#7 to PEM

```
openssl pkcs7 -print_certs -in certs.p7b -out certs.pem
```