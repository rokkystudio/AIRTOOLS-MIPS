# AIRTOOLS-MIPS v1.2.0

Первый тегированный релиз MIPS-части AIRTOOLS: прошивка `mtd4` для Wi-Fi
эндоскопа на MT7628 (management AP `AT`) с внешним TP-Link WN723N/RTL8188EUS
в monitor mode и TCP control API `/bin/airtools` версии 1.2.

## Что в релизе

- `mtd4_airtools_mips_v1.2.0.bin` — готовый образ раздела `Kernel/mtd4`,
  собран из базы `dumps/bases/mtd4_connectivity_base_20260916.bin`.
- `airtools_mipsel_v1.2.0`, `airodump_mipsel_v1.2.0`, `aireplay_mipsel_v1.2.0` —
  те же бинарники, что упакованы в образ (для отладки и сверки).
- `SHA256SUMS.txt` — контрольные суммы всех файлов.

## Изменения относительно прошлого проверенного образа

Прошлый физически проверенный milestone:
`mtd4_airtools_clients_replay_20260923.bin`
(`04863863b0bfbacd0439eb449e11422ef1db7aa3fd08d8a95edaa344629d265e`).

В v1.2.0 вошли:

- exact M1/M2 handshake pair — handshake публикуется только при паре
  M1 (ACK) и M2 (MIC) от одного BSSID;
- gate replay on capture readiness — `/replay` работает только при активном
  target capture и остановленном discovery hopper;
- AP metadata в handshake PCAP — beacon/probe response с ESSID пишется перед
  EAPOL-кадрами;
- runtime index клиентов `/tmp/airscan-clients.txt` и endpoint `/clients`;
- per-client replay через `/replay?station=<mac>`;
- `AIRTOOLS_VERSION 1.2` в ответе `/status`.

## Совместимость

- Устройство: эндоскоп MT7628, flash layout с `Kernel/mtd4` (3 866 624 байта).
- Monitor-адаптер: TP-Link WN723N / RTL8188EUS, драйвер `8188eu`.
- Android-клиент AIRTOOLS (AIRTOOLS-APP) — совместим по TCP API.
- Писать только `mtd4`; `mtd1` Bootloader, `mtd2` Config, `mtd3` Factory не трогать.

## Прошивка

Порядок и проверки описаны в `FIRMWARE.md`, правила безопасности и recovery —
в `BRICK.md`. Кратко:

```text
UART COM3 57600 8N1, TFTP-сервер с образом
mtd_write write <image> Kernel
проверить MTD_WRITE_RET:0 и SYNC_DONE
reboot только после успешной записи
```

## Статус проверки

- Образ собран builder-ом из HEAD (`9edc7ea`, `Update airtools replay API version`).
- Builder проверил размер `3 866 624`, uImage header CRC, uImage data CRC и
  наличие `airtools/airwifi/airodump/aireplay` в rootfs.
- **Аппаратная проверка именно этой сборки ещё не выполнялась** — после
  обновления API версии. Прошлый milestone `clients_replay_20260923` проверен
  на устройстве. Перед переносом в `dumps/verified` и использованием как
  «проверенного» прошейте образ и убедитесь в boot, AP `AT`, TCP/8088 и capture.

## SHA-256

- `mtd4_airtools_mips_v1.2.0.bin` — `4013eb9415de5082c8c34343f093f50f77b99c2cfd8c5598e2c80839e672dc91`
- `airtools_mipsel_v1.2.0` — `a3ae861bf5d328541ec96b5f110de61acdcb83b68d446e3fadc18c07b5203367`
- `airodump_mipsel_v1.2.0` — `d4a7abff9f1fd79950d6e11df46b24cfa5e52111bc1d02460d2bec1c8d62ecd3`
- `aireplay_mipsel_v1.2.0` — `0370320ce595c1c6d2295ce9ca06efbf75ebf544a0202ea18470ede0416751e2`
