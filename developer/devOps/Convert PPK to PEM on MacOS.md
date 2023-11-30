You can `ssh` directly from the Terminal on Mac, but you need to use a `.PEM` key rather than the `putty` `.PPK` key. You can use PuttyGen on Windows to convert from `.PEM` to `.PPK`, I'm not sure about the other way around though.

You can also convert the key using `putty` for Mac via `port` or `brew`:

```
sudo port install putty
```

or

```
brew install putty
```

This will also install `puttygen`. To get `puttygen` to output a `.PEM` file:

```
puttygen privatekey.ppk -O private-openssh -o privatekey.pem
```

Once you have the key, open a terminal window and:

```
ssh -i privatekey.pem user@my.server.com
```

The private key must have tight security settings otherwise SSH complains. Make sure only the user can read the key.

```
chmod go-rw privatekey.pem
```
