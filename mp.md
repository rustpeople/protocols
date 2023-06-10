# MP

Messaging Protocol.

# 1. Message Structure

```
version + req/res + header + body
```

# 2. MP version

The `version` part consists of 1 byte that indicates the version of MP being used. This document is only about version 1, 0x00.

# 3. Request/response indicator

The `req/res` part consists of 1 bit that indicates if the message is a request or response. Request = 0, response = 1.

# 4. Request Header Structure

```
command + arguments
```

# 5. Request Command List

The `command` part of a request header consists of 1 byte that indicates the command.

## JOIN, 0x00

A command to start the connection. It takes no arguments.

## QUIT, 0x01

A command to quit the connection. It takes no arguments.

## GETUSR, 0x02

A command to get the other device's username. It takes no arguments.

## SENDMSG, 0x03

A command to send a message to the other device. The message should be on the request body.

## SENDFILE, 0x04

A command to send a file to the other device. It takes the filename as argument, and the file's contents should be on the request body.

## GETUSRS, 0x05

A command to get other devices to connect with. It takes no arguments.

## GETSTATS, 0x06

A command to get the status of the other device. It takes no arguments.

# 6. Request/response body

The `body` part can contain any type of data with any length.

# 7. Response Header Structure

```
status-code
```

# 8. Status code list

The `status-code` part of a response header consists of 1 byte that indicates the response code.

## OK, 0x00

No error occurred.

# 9. Responses for each command

## JOIN, 0x00

Nothing.

## QUIT, 0x01

Nothing.

## GETUSR, 0x02

Only the username on the response body.

## SENDMSG, 0x03

Nothing.

## SENDFILE, 0x04

Nothing.

## GETUSRS, 0x05

Only a JSON list of devices to connect with on the response body.

## GETSTATS, 0x06

Only the status on the message body.

# 10. How to implement

The data is transfered on an UDP socket. The standard port is 5315.