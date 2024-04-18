# openwrt-feeds

- [silversearcher-ag](https://github.com/ggreer/the_silver_searcher)
- [mqtt-dissector](https://github.com/someburner/mqtt-dissector)

# Usage

1. Follow [openwrt sdk guide](https://openwrt.org/docs/guide-developer/toolchain/using_the_sdk)

2. Add feed to `feeds.conf.default`

```
src-git someburner https://github.com/someburner/openwrt-feeds.git
```

3. Update feeds

```sh
./scripts/feeds update -a
./scripts/feeds install mqtt-dissector
./scripts/feeds install silversearcher-ag
```

4. Select packages in menuconfig

```sh
make menuconfig

# > Custom Apps
# --> mqtt-dissector
# --> silversearcher-ag
# hit space to choose <M>
```

5. Compile

```sh
make package/mqtt-dissector/{clean,compile} V=s
make package/silversearcher-ag/{clean,compile} V=s
```
