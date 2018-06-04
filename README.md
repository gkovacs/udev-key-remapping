# udev-key-remapping

This is a set of files you can put into /etc/udev/hwdb.d/ and it will do things like turn your caplock key into backspace, on a per-keyboard basis.

## Generating your own

These were generated as follows:

Run

```bash
sudo evtest /dev/input/event4
```

You may need to replace event4 with event5 or so. Keep changing the number until you get to the one where when you press buttons on your target keyboard it prints out the key and scancode.

Look for the line that looks like

```
Input device ID: bus 0x5 vendor 0x46d product 0xb317 version 0x900
```

The above happens to be the line for the typematrix. Then you convert it into `evdev:input:b0005v046DpB317*` as follows

```
evdev:input:b${bus}v${vendor}p${product}
```

Where things in `${}` are the numbers from the `Input device ID:` line for that device, padded with leading 0s to be length 4 and capitalized.
