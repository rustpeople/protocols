# MUSIP

Music Transfer Protocol. Disclaimer: all music files must be in mp4.

# 1. Message Structure

```
version + req/res + req/res-header + req/res-body
```

# 2. MUSIP version

The `version` part consists of 1 byte that indicates the version of MUSIP being used. This document is only about version 1, 0x00.

# 3. Request/response indicator

The `req/res` part consists of 1 bit that indicates if the mesage is a request or response. Request = 0, response = 1.

# 4. Request Header Structure

```
command + arguments
```

# 5. Request Command List

The `command` part of a Request Header consists of 1 byte that indicates the command.

## JOIN, 0x00

A command to start the connection. It takes no arguments.

## QUIT, 0x01

A command to quit the connection. It takes no arguments.

## LIST, 0x02

A command to list all musics available. It takes no arguments.

## GET, 0x03

A command to get an specific music. It takes the music id as an argument (4 bytes).

## PUB, 0x04

A command to publish an specific music. It takes the music id as argument (4 bytes), and the music data is on the request body.

## SEE, 0x05

A command to see info about an specific music. It takes the music id as argument (4 bytes).

# 6. Request Body

The body of a request can contain any type of data.

# 7. Response Header Structure

```
status-code
```

# 8. Status Code List

The `status-code` part of a response header consists of 1 byte that indicates the response code.

## OK, 0x00

No error ocurred.

## 0x01

Permission denied.

## 0x02

Music id already exists.

## 0x03

Music id doesn't exist.

# 9. Responses for each command

## JOIN, 0x00

Nothing, only status code of 0x00 or 0x01.

## QUIT, 0x01

Nothing, only status code of 0x00.

## LIST, 0x02

Status code: 0x00 or 0x01. Message body: A list of music ids, that should not be separeted (because music ids have a defined size).

## GET, 0x03

Status code: 0x00, 0x01, or 0x03. Message body: the data contained inside the music file.

## PUB, 0x04

Status code: 0x00, 0x01 or 0x02. Message body: nothing.

## SEE 0x05

Status code: 0x00, 0x01 or 0x03. Message body: JSON data about the music, such as author and name.

# 10. How to implement

The data is transfered on an UDP socket. The standard port is 2215.