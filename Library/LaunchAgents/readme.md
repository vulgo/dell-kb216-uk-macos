# local.hidutil.Dell-KB216.plist

```launchd``` job that runs when Apple's HID driver matches on Dell KB216. ```xpc_set_event_stream_handler``` consumes the IOKit matching event and runs ```hidutil``` with arguments.

## xpc_set_event_stream_handler

See [https://github.com/snosrap/xpc_set_event_stream_handler](https://github.com/snosrap/xpc_set_event_stream_handler)

### Building

```
mkdir xpc_set_event_stream_handler
cd xpc_set_event_stream_handler
curl https://raw.githubusercontent.com/snosrap/xpc_set_event_stream_handler/master/xpc_set_event_stream_handler/main.m -o main.m
clang -framework Foundation -o xpc_set_event_stream_handler main.m
```

## hidutil

```
hidutil property --matching JSON --set JSON
```

Remap keys as in the following table targetting KB216 by product ID and vendor ID.

| Source |                       | Destination |           |
|-------:|:----------------------|------------:|:----------|
| 0xe2   | Left Alt              | 0xe3        | Left GUI  |
| 0xe3   | Left GUI              | 0xe2        | Left Alt  |
| 0xe6   | Right Alt             | 0xe7        | Right GUI |
| 0x65   | Application / Compose | 0xe6        | Right Alt |
| 0x49   | Insert                | 0x6b        | F16       |

[HID Usage Tables on usb.org (PDF)](https://www.usb.org/sites/default/files/documents/hut1_12v2.pdf)
### --matching

```
{
	"ProductID": 0x2113,
	"VendorID": 0x413c
}
```

### --set

```
{
	"UserKeyMapping": [
		{
			"HIDKeyboardModifierMappingSrc":0x7000000e2,
			"HIDKeyboardModifierMappingDst":0x7000000e3
		},{
			"HIDKeyboardModifierMappingSrc":0x7000000e3,
			"HIDKeyboardModifierMappingDst":0x7000000e2
		},{
			"HIDKeyboardModifierMappingSrc":0x7000000e6,
			"HIDKeyboardModifierMappingDst":0x7000000e7
		},{
			"HIDKeyboardModifierMappingSrc":0x700000065,
			"HIDKeyboardModifierMappingDst":0x7000000e6
		},{
			"HIDKeyboardModifierMappingSrc":0x700000049,
			"HIDKeyboardModifierMappingDst":0x70000006b
		}
	]
}
```
