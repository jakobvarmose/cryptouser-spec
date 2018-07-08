---
title: Database
permalink: /docs/database/
layout: page
---

The database consists of two tables.

## users table

|--------------|--------------|---|---|---|---|---|---|
|id            |varbinary(255)|   |   |   |   |   |   |
|username      |varbinary(255)|   |   |   |   |   |   |
|saltinfo      |mediumblob    |   |   |   |   |   |   |
|read_key_hash |varbinary(255)|   |   |   |   |   |   |
|write_key_hash|varbinary(255)|   |   |   |   |   |   |
|root_key_hash |varbinary(255)|   |   |   |   |   |   |
|created_at    |timestamp     |   |   |   |   |   |   |
|accessed_at   |timestamp     |   |   |   |   |   |   |
|updated_at    |timestamp     |   |   |   |   |   |   |

### id

The id identifying this data.

### read_key_hash

The read_key hashed with SHA-256.

### write_key_hash (append_key?)

The write_key hashed with SHA-256. Used for appending new versions of the private (and public?) data.

### root_key_hash (delete_key?/write_key?)

The root_key hashed with SHA-256. The root_key is used for modifying read_key, write_key, root_key and public.

### created_at

Initial time this item was created.

### accessed_at

Last time the private_encrypted data was successfully fetched.

### updated_at

Last time this item was successfully updated.

### saltinfo


## versions table

|--------------|--------------|
|id            |varbinary(255)|
|user_id       |varbinary(255)|
|updated_at    |timestamp     |
|private_enc/protected   |mediumblob    |

### id

### user_id

### updated_at

When this version was created or deleted.

### public

The public data supplied by the client. This data is available to anyone who knows the id.

### protected

Data that is available to both the server and client. This data is available to anyone who knows the read_key.

### private_enc

The encrypted private data as supplied by the client. This data is available to anyone who knows the read_key.

A malicious server may send an old or invalid private_enc, but cannot directly modify the content.

|                   |  delete_key | append_key | read_key | without a key |
|-------------------|------------|------------|----------|---------------|
| **user**              |  delete |         |   | create             |
| .hashinfo            | write |         |   | read             |
| .delete_key_hash     |  write      |            |   |               |
| .append_key_hash     |  write      |            |   |               |
| .read_key_hash       |  write      |            |   |               |
| .created_at         |       |        | read |   |
| .accessed_at         |        |        | read |   |
| .updated_at          |        |        | read |               |
| **version**         | delete | create |   |              |
| .created_at    |  read all |  | read latest |            |
| .public      |  read all |  |  read latest | read latest |
| .protected   |  read all  |  | read latest |               |
| .private_enc |  read all  |  | read latest |               |
| .private     |  read all |  | read latest** |               |

\* The decryption key is also needed.


## 

## blocks table

### id

Randomly generated id of this block.

### updated_at

When this block was created or deleted.

### read_key_hash

The read_key hashed with SHA-256.

### private_encrypted

The encrypted private data as supplied by the client. Only clients who know the read_key can fetch this data.






