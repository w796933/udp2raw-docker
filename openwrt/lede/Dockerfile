FROM yhnw/openwrt-sdk:lede-ar71xx
ARG REV=master
COPY \
  openwrt/common/Makefile.openwrt \
  openwrt/common/udp2raw.init \
  openwrt/common/udp2raw.conf /
RUN \
  cd /home/openwrt/sdk && \
  mkdir -p package/udp2raw && \
  if ! [ -z $REV ]; then \
    sed -i "s/PKG_SOURCE_VERSION:=.*/PKG_SOURCE_VERSION:=$REV/g" /Makefile.openwrt; \
  fi; \
  cp /Makefile.openwrt package/udp2raw/Makefile && \
  cp /udp2raw.conf package/udp2raw/ && \
  cp /udp2raw.init package/udp2raw/ && \
  su openwrt -c "make defconfig && make package/udp2raw/compile" && \
  cp bin/packages/mips_24kc/base/udp2raw*.ipk /udp2raw-lede-ar71xx.ipk && \
  cp build_dir/target-*/udp2raw/udp2raw-*/udp2raw /udp2raw-lede-ar71xx && \
  tar --xform="s%^%udp2raw-${REV}/%" -zcvf /bin.tgz /udp2raw-lede-ar71xx.ipk /udp2raw-lede-ar71xx
