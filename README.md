# GPG


## Create a key

```bash
gpg --full-generate-key
```

## Export a public key

```bash
gpg --export -a "User Name"
# or
gpg --export -a "User Name" > public.key
```

This will create a file called public.key with the ascii representation of the public key for User Name.

## Export a private key

```bash
gpg --export-secret-key -a "User Name" > private.key
```

This will create a file called private.key with the ascii representation of the private key for User Name.
It's pretty much like exporting a public key, but you have to override some default protections. There's a note (*) at the bottom explaining why you may want to do this.

## Import a public key

```bash
gpg --import public.key
```


## Delete a public key (from your public key ring)

```bash
gpg --delete-key "User Name"
```

This removes the public key from your public key ring.

> NOTE! If there is a private key on your private key ring associated with this public key, you will get an error! You must delete your private key for this key pair from your private key ring first.

## Delete an private key (a key on your private key ring)

```bash
gpg --delete-secret-key "User Name"
```
This deletes the secret key from your secret key ring.

## List the keys in your public key ring

```bash
gpg --list-keys
```

## To list the keys in your secret key ring

```bash
gpg --list-secret-keys
```

## Fingerprint

To generate a short list of numbers that you can use via an alternative method to verify a public key, use:

```bash
gpg --fingerprint > fingerprint
```

This creates the file fingerprint with your fingerprint info.

## Encrypt data

```bash
gpg -e -u "Sender User Name" -r "Receiver User Name" mydata
```

There are some useful options here, such as -u to specify the secret key to be used, and -r to specify the public key of the recipient.

## Decrypt data

```bash
gpg -d mydata.tar.gpg
```


## Send key to remote keyserver

[https://keyring.debian.org](https://keyring.debian.org/)

```bash
gpg --keyserver keyring.debian.org --send-key user@email.com
```


## Get key from remote keyserver

```bash
gpg --keyserver keyring.debian.org --recv-key 0xBB7576AC
```

## Change key expiration

- http://www.g-loaded.eu/2010/11/01/change-expiration-date-gpg-key/

https://www.debian.org/events/keysigning.pt.html


## Git

```bash
# Someone trying to pass another username and email
git commit --amend --author="Author Name <email@address.com>" --no-edit

# Signing commits
git commit -m "some message" -S
git log --show-signature

git verify-commit

git verify-tag
```

#### ~/.gitconfig
```
[user]
	email = arthurbdiniz@gmail.com
	name = Arthur Diniz
	signingkey = arthurbdiniz@gmail.com

[commit]
	gpgsign = true

[tag]
	gpgSign = true

[init]
        defaultBranch = main
```