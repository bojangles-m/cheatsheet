## RSA SSH keys

If you use RSA keys for SSH, the US National Institute of Standards and Technology recommends
that you use a key size of at least 2048 bits.
By default, the ssh-keygen command creates an 1024-bit RSA key.

You can create and configure an RSA key with the following command, substituting if desired for the minimum recommended key size of 2048:

```
ssh-keygen -t rsa -b 2048 -C "email@example.com"
```

The -C flag, with a quoted comment such as an email address, is an optional way to label your SSH keys.

You'll see a response similar to:

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa):
```

##Testing that everything is set up correctly

To test whether your SSH key was added correctly, run the following command in
your terminal (replacing gitlab.com with your GitLab's instance domain):

```
ssh -T git@gitlab.com
```

The first time you connect to GitLab via SSH, you will be asked to verify the
authenticity of the GitLab host that you're connecting to.
For example, when connecting to GitLab.com, answer yes to add GitLab.com to
the list of trusted hosts:

```
The authenticity of host 'gitlab.com (35.231.145.151)' can't be established.
ECDSA key fingerprint is SHA256:HbW3g8zUjNSksFbqTiUWPWg2Bq1x8xdGUrliXFzSnUw.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'gitlab.com' (ECDSA) to the list of known hosts.
```

Once added to the list of known hosts, you won't be asked to validate the
authenticity of GitLab's host again. Run the above command once more, and
you should only receive a Welcome to GitLab, @username! message.

If the welcome message doesn't appear, you can troubleshoot the problem by running ssh
in verbose mode with the following command:

```
ssh -Tvvv git@gitlab.com
```

## Link the key to your global git configuration (Telling Git about your signing key)

If you are missing GPG install it with homebrew

```
brew install gnupg
```

If getting error: gpg failed to sign the data then:
GPG uses pinentry to prompt you for your passphrase. If you're not seeing any prompt, you may need a different pinentry program:

1. Install GUI version

```sh
brew install pinentry-mac
```

2. Then update your GPG config

```sh
echo "pinentry-program /opt/homebrew/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf
```

3. Then reload GPG agent

```sh
gpgconf --kill gpg-agent
gpgconf --launch gpg-agent
```

### Generate a new GPG key from hidden email address

your github email: https://github.com/settings/emails
new GPG key: https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key

### Adjust git global config

```
git config --global --list

git config --global <prop> <value>

git config --global user.name "<name>"
git config --global user.signingkey "<gpg key>"
git config --global user.email "<github email>"
git config --global commit.gpgsign true
git config --global pull.rebase false
git config --global init.defaultbranch main

# Enable default commit signing via the CLI
git config --global gpg.program gpg

```

## Working with non-default SSH key pair paths

If you used a non-default file path for your GitLab SSH key pair configure your SSH client to point to your GitLab private SSH key. To make these changes, run the following commands:

```
eval $(ssh-agent -s)
ssh-add <path to private SSH key>
```

Now save these settings to the ~/.ssh/config file. Two examples for SSH keys dedicated to GitLab are shown here:

```
# GitLab.com
Host gitlab.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/gitlab_com_rsa
```

```
# Private GitLab instance
Host gitlab.company.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/example_com_rsa
```

Public SSH keys need to be unique to GitLab, as they will bind to your account.

Your SSH key is the only identifier you'll have when pushing code via SSH, that's why it needs to uniquely map to a single user.
