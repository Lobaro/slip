# slip go
Implementation of [SLIP (rfc-1055)](https://tools.ietf.org/html/rfc1055) in GoLang

In addition to the basic SLIP reader and writer there is also a SlipMux implementation, that enables sending different packet types like CoAP and Diagnostic messages. This implemented backward compatible to SLIP implementations which support only IP packets.

If needed further packet types can be implemented by the use of the library.

# Install

```
go get -u github.com/Lobaro/slip
```


# Usage

```
import github.com/Lobaro/slip
```

Read Packets
```
	data := []byte{1, 2, 3, slip.END}
	reader := slip.NewReader(bytes.NewReader(data))
	packet, isPrefix, err := reader.ReadPacket()

	// packet == [1, 2, 3]
	// isPrefix == false
	// err == io.EOF
```

Write Packets
```
	buf := &bytes.Buffer{}
	writer := slip.NewWriter(buf)
	err := writer.WritePacket([]byte{1, 2, 3})

	// buf.Bytes() ==  [END, 1, 2, 3, END]
```
