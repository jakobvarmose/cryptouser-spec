---
title: API
permalink: /docs/api/
layout: page
---

This page explains how to interact with a server implementing the CryptoUser API.

### GET /.well-known/cryptouser/version

Successful response: `{ version: 1 }`

Error response: *anything else*

Check if this server supports the CryptoUser API.

### POST /.well-known/cryptouser/create_user

Request: `{ username, saltinfo, access_key, protected }`

Successful response: `{}`

Error response: `{ error }`

Create a new user.

### POST /.well-known/cryptouser/get_saltinfo

Request: `{ username }`

Successful response: `{ saltinfo }`

Error response: `{ error }`

Read saltinfo in order to log in.

### POST /.well-known/cryptouser/get_protected

Request: `{ username }`

Authorization: `access_key`

Successful Response: `{ protected }`

Error response: `{ error }`

Read protected data when logging in.

### POST /.well-known/cryptouser/update_user

Request: `{ username, saltinfo, access_key, protected }`

Authorization: `access_key`

Successful response: `{}`

Error response: `{ error }`

Update keys, saltinfo and protected data.

### POST /.well-known/cryptouser/delete_user

Request: `{ username }`

Authorization: `access_key`

Successful response: `{}`

Error response: `{ error }`

Delete a user.