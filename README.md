go-syslog 
==============================

Fork of [Máximo Cuadros go-syslog](https://github.com/mcuadros/go-syslog).

Changed *Handler* interface- raw syslog message added as first argument to Handle:
```go
type Handler interface {
	Handle([]byte, format.LogParts, int64, error)
}
```

Syslog server library for go, build easy your custom syslog server over UDP, TCP or Unix sockets using RFC3164, RFC6587 or RFC5424

Installation
------------

The recommended way to install go-syslog

```
go get github.com/g41797/go-syslog
```

Examples
--------

How import the package

```go
import "github.com/g41797/go-syslog"
```

Example of a basic syslog [UDP server](example/basic_udp.go):

```go
channel := make(syslog.LogPartsChannel)
handler := syslog.NewChannelHandler(channel)

server := syslog.NewServer()
server.SetFormat(syslog.RFC5424)
server.SetHandler(handler)
server.ListenUDP("0.0.0.0:514")
server.Boot()

go func(channel syslog.LogPartsChannel) {
    for logParts := range channel {
        fmt.Println(logParts)
    }
}(channel)

server.Wait()
```

License
-------

MIT, see [LICENSE](LICENSE)
