# 代码雨命令cmatrix

cmztrix命令

```text
 Usage: cmatrix -[abBfhlsVx] [-u delay] [-C color]
 -a: Asynchronous scroll
 -b: Bold characters on
 -B: All bold characters (overrides -b)
 -f: Force the linux $TERM type to be on
 -l: Linux mode (uses matrix console font)
 -o: Use old-style scrolling
 -h: Print usage and exit
 -n: No bold characters (overrides -b and -B, default)
 -s: "Screensaver" mode, exits on first keystroke
 -x: X window mode, use if your xterm is using mtx.pcf
 -V: Print version information and exit
 -u delay (0 - 10, default 4): Screen update delay
 -C [color]: Use this color for matrix (default green)
```

支持的颜色 Valid colors are `green, red, blue, white, yellow, cyan, magenta and black`.

{% file src="../../.gitbook/assets/cmatrix.bin" caption="cmztrix可执行文件" %}

[github源码地址](https://github.com/abishekvashok/cmatrix)

