### Generate random 32-bytes base64-encoded secret and copy directly on your clipboard.

```shell
$ openssl rand -base64 32 | pbcopy
```

### Use "pbcopy" to copy content of file to your clipboard.

```shell
$ pbcopy < file.txt
```

### You can check if the content is there by using the "pbpaste" command:

```shell
$ pbpaste
```
