# Артефакты

Эта папка хранит полезные результаты сборок и внешние бинарники, которые нельзя держать в disposable `build`.

## Firmware Images

```text
dumps\original\   заводские recovery dumps
dumps\bases\      стабильные base images для пересборки
dumps\verified\   проверенные прошитые images
```

Текущий релизный образ:

```text
dumps\verified\mtd4_airtools_mips_v1.2.0.bin
size:   3866624
sha256: 4013eb9415de5082c8c34343f093f50f77b99c2cfd8c5598e2c80839e672dc91
```

Base image для WN723N/airtools builder:

```text
dumps\bases\mtd4_connectivity_base_20260916.bin
```

## Binary Artifacts

```text
artifacts\binaries\mipsel\
  airapi_mipsel
  aireplay_mipsel
  airodump_mipsel
  airtools_mipsel
  airwifi
  endoscope-connectivity
  mtd4_lzma_extract_8188eu_mipsel
  rtap_capture_mipsel
  rtap_pcap_capture_mipsel

artifacts\drivers\rtl8188eus\
  8188eu_vendorabi_pm_skb_slim.ko
  8188eu_vendorabi_pm_skb_slim.ko.lzma

artifacts\vendor\
  mt_wifi.ko

artifacts\windows\
  AT-open-profile.xml
  ch341_driver_export\
```

`build\` теперь считается disposable output и игнорируется Git.
