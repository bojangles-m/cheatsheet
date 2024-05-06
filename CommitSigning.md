# Commit Signing

# Install dependencies

```shell
$ brew install gpg
$ brew install pinentry-mac

$ mkdir ~/.gnupg
```

Double check the path for pinentry-mac with:

```shell
$ which pinentry-mac
```

```shell
$ echo "pinentry-program <path to pinentry-mac>" >> ~/.gnupg/gpg-agent.conf
$ killall gpg-agent

```

# Generate a GPG key

Generate a GPG key pair. Since there are multiple versions of GPG, you may need to consult the relevant man page to find the appropriate key generation command. Your key must use RSA.

```shell
$ gpg --default-new-key-algo rsa4096 --gen-key
```

- At the prompt, specify the kind of key you want, or press Enter to accept the default.
- At the prompt, specify the key size you want, or press Enter to accept the default. Your key must be at least 4096 bits.
- Enter the length of time the key should be valid. Press Enter to specify the default selection, indicating that the key doesn't expire.
- Verify that your selections are correct.
- Enter your user ID information.

  ***

  **NOTE**

  When asked to enter your email address, ensure that you enter the verified email address for your GitHub account. To keep your email address private, use your GitHub-provided no-reply email address. For more information, see "Verifying your email address" and "Setting your commit email address."

  ***

- Type a secure passphrase.
- From the list of GPG keys, copy the long form of the GPG key ID you'd like to use. In this example, the GPG key ID is 3AA5C34371567BD2:

  ```
  $ gpg --list-secret-keys --keyid-format=long
  /Users/hubot/.gnupg/secring.gpg
  ------------------------------------
  sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
  uid                          Hubot
  ssb   4096R/42B317FD4BA89E7A 2016-03-10

  ```

- Export the gpg public key block. In this example, the GPG key ID is 3AA5C34371567BD2:

  ```
  $ gpg --armor --export 3AA5C34371567BD2
  # Prints the GPG key ID, in ASCII armor format
  ```

- Copy your GPG key, with beginning and end block

  ```
  -----BEGIN PGP PUBLIC KEY BLOCK-----
  ...
  ...

  -----END PGP PUBLIC KEY BLOCK-----
  ```

# Adding a new GPG key to your GitHub account

Github Avatar -> Settings -> SSH and GPG keys -> New GPG key -> copy the Block

# Telling Git about your GPG key

Use the gpg command to list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.

```shell
  $ gpg --list-secret-keys --keyid-format=long
  /Users/hubot/.gnupg/secring.gpg
  ------------------------------------
  sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
  uid                          Hubot
  ssb   4096R/42B317FD4BA89E7A 2016-03-10

```

To set your GPG signing key in Git, paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is 3AA5C34371567BD2!

```shell
$ git config --global user.signingkey [GPG key ID]
```

# To enable commit signing in VS Code

```shell
$ git config --global gpg.program true
$ git config --global commit.gpgsign true
```

# Useful GPG commands

```shell
$ gpg --list-keys
$ gpg --delete-key [uid]

$ gpg --list-secret-keys
$ gpg --delete-secret-key [uid]
```
