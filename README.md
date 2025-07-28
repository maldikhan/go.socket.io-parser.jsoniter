# Socket.IO V5 Default Event Payload Parser with Jsoniter

This package provides a high-performance JSON parser for [Socket.IO V5](https://github.com/maldikhan/go.socket.io) protocol event payload using the [jsoniter](https://github.com/json-iterator/go) library. It's designed to be a drop-in replacement for the default JSON parser, offering significant performance improvements.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/maldikhan/go.socket.io-parser.jsoniter/blob/main/LICENSE)
[![Go Report Card](https://goreportcard.com/badge/github.com/maldikhan/go.socket.io-parser.jsoniter#latest)](https://goreportcard.com/report/github.com/maldikhan/go.socket.io-parser.jsoniter)
[![codecov](https://codecov.io/github/maldikhan/go.socket.io-parser.jsoniter/branch/master/graph/badge.svg?token=dWuUXfFPr4)](https://codecov.io/github/maldikhan/go.socket.io-parser.jsoniter)
[![Go Reference](https://pkg.go.dev/badge/github.com/maldikhan/go.socket.io-parser.jsoniter.svg)](https://pkg.go.dev/github.com/maldikhan/go.socket.io-parser.jsoniter)  
[![Test](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/test.yaml/badge.svg)](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/test.yaml)
[![Lint](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/lint.yaml/badge.svg)](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/lint.yaml)
[![Sec](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/security.yaml/badge.svg)](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/security.yaml)
[![CodeQL](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/github-code-scanning/codeql/badge.svg)](https://github.com/maldikhan/go.socket.io-parser.jsoniter/actions/workflows/github-code-scanning/codeql)

## Features

- High-performance JSON parsing and serialization
- Compatible with [Socket.IO V5](https://github.com/maldikhan/go.socket.io) default protocol parser
- Easy integration with the default parser

## Installation

To use this parser, first ensure you have the main [Socket.IO](https://github.com/maldikhan/go.socket.io) client library installed:

```sh
go get github.com/maldikhan/go.socket.io
```

Then, install this parser:

```sh
go get github.com/maldikhan/go.socket.io-parser.jsoniter
```

## Usage

To use this parser with the Socket.IO client, you need to create a new parser instance and pass it to the client constructor:

```go
package main

import (
    "github.com/maldikhan/go.socket.io"
    socketio_v5_parser_default "github.com/maldikhan/go.socket.io/socket.io/v5/parser/default"
    socketio_v5_parser_default_jsoniter "github.com/maldikhan/go.socket.io-parser.jsoniter"
    "github.com/maldikhan/go.socket.io/utils"
)

func main() {
    client, err := socketio.NewClient(
        socketio.WithRawURL("http://localhost:3000"),
        socketio.WithParser(socketio_v5_parser_default.NewParser(
            socketio_v5_parser_default.WithLogger(&utils.DefaultLogger{Level: utils.WARN}),
            socketio_v5_parser_default.WithPayloadParser(socketio_v5_parser_default_jsoniter.NewPayloadParser(
                socketio_v5_parser_default_jsoniter.WithLogger(&utils.DefaultLogger{Level: utils.WARN}),
            )),
        )),
    )
    if err != nil {
        // Handle error
    }
    
    // Use the client as normal
    /*
        err := client.Connect(ctx)
        ...
    */
}
```

## Performance

This parser can provide 2-4x faster parsing of payloads compared to the standard library's `encoding/json`. The exact performance gain may vary depending on your specific use case and payload structure.

## Compatibility

This parser is designed to be fully compatible with the Socket.IO V5 protocol. It can be used as a drop-in replacement for the default parser without any changes to your existing code.

## Contributing

Contributions to improve the parser are welcome. Please feel free to submit issues or pull requests.

## Acknowledgments

- [Socket.IO](https://socket.io/) for the original protocol and implementation
- [jsoniter](https://github.com/json-iterator/go) for fast JSON parsing

## License

This parser is licensed under the MIT License. See the [LICENSE](./LICENSE) file in the root of the repository for the full license text.
