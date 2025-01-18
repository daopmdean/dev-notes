## Protocol Properties
protocols designed to solve problems

- data format
	- text base: json, xml,...
	- binary: protobuf, resp, h2,...
- transfer mode
	- message based: udp, http
	- stream: tcp, webRTC
- addressing system
	- dns name, ip, mac
- directionality
	- bidirectional: tcp
	- unidirectional: http
	- full/half duplex
- state
	- stateful: tcp, gRPC, apache thrift
	- stateless: udp, http
- routing
	- proxies, gateways
- flow & congestion control
	- tcp: flow & congestion
	- udp: no control
- error management
	- error code
	- retries and timeouts

## OSI Models

Open System Interconnection model

- layer 7 - application - http/FTP/gRPC
- layer 6 - presentation - encoding, serialization
- layer 5 - session - connection establishment, TLS
- layer 4 - transport - UDP/TCP
- layer 3 - network - IP
- layer 2 - data link - frames, mac address ethernet
- layer 1 - physical - electric signals, fiber or radio waves