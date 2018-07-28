---
title: Overview
permalink: /docs/overview/
layout: page
---

CryptoUser is a system to create webservices where the user can store information, but all information is encrypted so the server doesn't know anything about what is being stored.

The information is first encrypted by the client and is then encrypted with a key derived from the client's password and sent to the server to be stored. In order to make brute force attacks harder the encrypted data will only be sent back when the client provides an access key also derived from the password.

The server should hash the access key before storage. This ensures that even if the server data is leaked to a third party they cannot modify any user data.
