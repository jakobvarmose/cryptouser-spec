---
title: Client
permalink: /docs/client/
layout: page
---

This page explains how the CryptoUser client works.

## Register

1. Get `server`, `username` and `password` from the user
2. Let `plaintext` be the initial user data
3. `salt = SHA256('1\0'+server+'\0'+username)`
4. `master_key = hash(username, password)`
5. `access_key = HKDF(master_key, 'x', 'y')`
6. `encryption_key = HKDF(master_key, 'x', 'y')`
7. `ciphertext = encrypt(encryption_key, plaintext)`
8. `saltinfo = '{"version":"1"}'`
9. Call /create_user
  * username: `username`
  * saltinfo: `saltinfo`
  * access_key: `access_key`
  * ciphertext: `ciphertext`

## Log in

1. Get `username` and `password` from the user
2. Call /get_public?username=`username`
3. TODO

## Log out

1. Delete the `server`, `username` and `master_key` variables.

## Update a user

1. TODO

## Delete a user

1. `access_key = HKDF(master_key, 'x', 'y')`
2. Call /delete_user
  * username: `username`
  * auth_access_key: `access_key`

