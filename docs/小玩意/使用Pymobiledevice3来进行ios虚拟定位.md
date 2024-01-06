## 使用Pymobiledevice3来进行ios虚拟定位

1. 先安装插件

```bash
python3 -m pip install -U pymobiledevice3
```

2. 创建tunnels

```bash
sudo python3 -m pymobiledevice3 remote start-tunnel
```

需要 root 权限，因为这将创建一个新的 TUN/TAP 设备，这是一项高权限操作。输出应该类似于：

```bash
Interface: utun6
RSD Address: fd7b:e5b:6f53::1
RSD Port: 64337
Use the follow connection option:
--rsd fd7b:e5b:6f53::1 64337
```

记录下这里的RSD地址和RSD接口，后面会用到。

3. 挂载Developer Disk Image & 开始虚拟定位

使用下面的命令挂载Developer Disk Image：

```bash
sudo pymobiledevice3 mounter auto-mount
```

随后，就可以使用下面的命令进行虚拟定位：

```bash
pymobiledevice3 developer dvt simulate-location set --rsd <HOST> <PORT> -- x y
```

其中，`<HOST>`和`<PORT>`就是上面记录的RSD地址和RSD接口，`x`和`y`是经纬度坐标。根据自行的需要替换即可。

更多用法

```
Usage: python -m pymobiledevice3 [OPTIONS] COMMAND [ARGS]...

Options:
  -h, --help  Show this message and exit.

Commands:
  activation       activation options
  afc              FileSystem utils
  amfi             amfi options
  apps             application options
  backup2          backup utils
  bonjour          bonjour options
  companion        companion options
  crash            crash report options
  developer        developer options.
  diagnostics      diagnostics options
  lockdown         lockdown options
  mounter          mounter options
  notification     notification options
  pcap             sniff device traffic
  power-assertion  Create a power assertion (wraps...
  processes        processes cli
  profile          profile options
  provision        privision options
  remote           remote options
  restore          restore options
  springboard      springboard options
  syslog           syslog options
  usbmux           usbmuxd options
  webinspector     webinspector options
  version          get installed package version
```

参考：

1. https://shawnhuang.io/posts/ios-17-location-simulation/
2. https://github.com/RManLuo/FakePosition
3. https://github.com/doronz88/pymobiledevice3