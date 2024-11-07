## ircserv
### About the 42 Norm:
- The project must be written (almost) solely in C++98.
- Any crash, leak, or conditional jump is forbidden.
- Allowed external functions are: everything in C++98,
                                  `socket`, `close`, `setsockopt`, `getsockname`,
                                  `getprotobyname`, `gethostbyname`, `getaddrinfo`,
                                  `freeaddrinfo`, `bind`, `connect`, `listen`, `accept`, `htons`,
                                  `htonl`, `ntohs`, `ntohl`, `inet_addr`, `inet_ntoa`, `send`,
                                  `recv`, `signal`, `sigaction`, `lseek`, `fstat`, `fcntl`, `poll`

### Project Overview:
This project aims to create **our own IRC server**. IRC is a text-based communication protocol, which offers real-time messaging that can be either public or private. Users can exchange
direct messages and join group channels on servers.

In order to replicate an IRC server we had to thoroughly follow the **norm** which rules this protocol.
Many versions are available, thus we chose to follow something in between [RFC 1459](https://www.rfc-editor.org/rfc/rfc1459.html) and [RFC 2812](https://www.rfc-editor.org/rfc/rfc2812) for implementation purposes.
Our project is designed to work with the **Hexchat** client, however it is also possible to use it with **netcat** by sending correctly formatted messages.

The way the project is designed makes it viable for users with low bandwidth, as we are not sending any messages until we received a combination of CR+LF (Carriage Return + Line Feed), meaning the end of the client's message.

Our server needs to be able to accept multiple clients at the same time using `poll` to listen for input in different fds.

It is possible to authenticate, set a nickname, a username, join a channel, send and receive private messages, set clients as operators or regular users and use the following commands with their arguments : `KICK`, `INVITE`, `TOPIC`, `MODE -+itkol`

This was a group project with my teammate [kprigent](https://github.com/nedulk), and we divided our work as the following :
- networking, client management, command recognition and the bot client were made by kprigent
- channel management and commands implementation were my part

As for the bonus part, we were asked to make file transfer possible and developing a bot client of our own.
