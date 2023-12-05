---
title: jets encrypted:edit
reference: true
---

## Usage

    jets encrypted:edit [options]

## Description

## Storing Encrypted Files in Source Control

The Jets `encrypted` commands provide access to encrypted files or configurations.
See the `Jets.application.encrypted` documentation for using them in your app.

This is a more generalized concept of `jets credentials`.

## Encryption Keys

By default, Jets looks for the encryption key in `config/master.key` or
`ENV["JETS_MASTER_KEY"]`, but that lookup can be overridden with `--key`:

    jets encrypted:edit config/encrypted_file.yml.enc --key config/encrypted_file.key

Don't commit the key! Add it to your source control's ignore file. If you use
Git, Jets handles this for you.

## Editing Files

To edit or create an encrypted file use:

    jets encrypted:edit config/encrypted_file.yml.enc

This opens a temporary file in `$EDITOR` with the decrypted contents for editing.

## Viewing Files

To print the decrypted contents of an encrypted file use:

    jets encrypted:show config/encrypted_file.yml.enc

## Access in App

Let's say you have encrypted like so:

    ❯ jets encrypted:show config/encrypted_file.yml.enc
    cloud:
      foo: bar

You can access them in the app like so:

    $ jets console
    > file = ActiveSupport::EncryptedFile.new(content_path: "./config/encrypted_file.yml.enc", key_path: "./config/master.key", env_key: Jets.env, raise_if_missing_key: true)
    > YAML.load(file.read)
    => {"cloud"=>{"foo"=>"bar"}}
    >

## Options

```
-k, [--key=KEY]  # The Jets.root relative path to the encryption key
                 # Default: config/master.key
```

