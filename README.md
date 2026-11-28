# AetherVPN

<p align="center">
  <img src="assets/logo.png" alt="AetherVPN" width="120" />
</p>

<p align="center">
  <a href="https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest"><img src="https://img.shields.io/github/v/release/keenfolk1-lgtm/aethervpn-releases?label=release&color=2ea44f" alt="Release" /></a>
  <a href="https://www.virustotal.com/gui/file/c0576efa796e22e4fbb5ed6b3c0b1d84408f396d2128f43c54802b4095e196e5"><img src="https://img.shields.io/badge/VirusTotal%20Android-0%2F67%20clean-2ea44f" alt="VirusTotal Android" /></a>
  <a href="https://www.virustotal.com/gui/file/32a6ac3da3847349527580f637f2a964759ef0d89e5ae0494449db6d0987690b"><img src="https://img.shields.io/badge/VirusTotal%20Windows-check%20report-2ea44f" alt="VirusTotal Windows" /></a>
  <a href="https://t.me/AetherAccessBot"><img src="https://img.shields.io/badge/Telegram-@AetherAccessBot-26A5E4" alt="Telegram Bot" /></a>
</p>

Клиент AetherVPN для Android и Windows. В этом репозитории публикуются готовые сборки и контрольные суммы SHA-256, исходный код закрыт.

## Скачать (v2.1.2)

Актуальные файлы лежат в разделе [Releases](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest):

- [AetherVPN-Android.apk](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest/download/AetherVPN-Android.apk) (Android, ARM64 и x86_64)
- [AetherVPN-Windows.exe](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest/download/AetherVPN-Windows.exe) (Windows 10/11 x64)
- [SHA256SUMS.txt](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest/download/SHA256SUMS.txt)

Доступ и ссылка подписки выдаются в Telegram-боте [@AetherAccessBot](https://t.me/AetherAccessBot): первые 24 часа бесплатно, дальше 100 ₽/мес (до 5 устройств). Вопросы по работе и оплате можно писать в [@maximka_sem](https://t.me/maximka_sem).

## Преимущества и устройство

AetherVPN работает на собственном закрытом протоколе, отличном от массовых VLESS, WireGuard и OpenVPN. Трафик маскируется под стандартные сессии TLS 1.3 и UDP/QUIC с гибридным постквантовым обменом ключами X25519 + ML-KEM.

- При резке скорости на 16 КБ или блокировке одного из каналов клиент автоматически переключается на резервный транспорт без ручной перенастройки.
- Раздельный туннель для РФ (RU Split-Tunnel) включен по умолчанию: российские банки, Госуслуги и локальные сайты открываются напрямую, отключать VPN ради них не приходится.
- Одна ссылка подписки объединяет все серверы (сейчас доступны Швеция и Австрия, Вена). Новые локации и сменные маршруты подтягиваются одной кнопкой обновления внутри приложения.
- Нативные клиенты под Android и Windows без тяжелых сторонних оболочек и рекламы, с одновременной работой до 5 устройств на одной подписке.

## Как подключиться

### Android

1. Скачайте `AetherVPN-Android.apk` и установите приложение.
2. Возьмите ссылку подписки в [@AetherAccessBot](https://t.me/AetherAccessBot).
3. Вставьте ссылку в приложении и нажмите кнопку подключения.

### Windows

1. Скачайте `AetherVPN-Windows.exe` и запустите от имени администратора (права нужны для системного TUN-интерфейса).
2. Если Windows SmartScreen покажет предупреждение о неизвестном издателе, нажмите "Подробнее", затем "Выполнить в любом случае".
3. Вставьте ссылку подписки из [@AetherAccessBot](https://t.me/AetherAccessBot) и подключитесь.

## Проверка файлов и VirusTotal

После скачивания сверьте контрольную сумму SHA-256 с файлом `SHA256SUMS.txt`:

```powershell
Get-FileHash .\AetherVPN-Windows.exe -Algorithm SHA256
```

Результаты проверки сборки v2.1.2:

- `AetherVPN-Android.apk`: **0/67** (чисто у всех антивирусов) | [отчет VirusTotal](https://www.virustotal.com/gui/file/c0576efa796e22e4fbb5ed6b3c0b1d84408f396d2128f43c54802b4095e196e5) | SHA-256 `c0576efa796e22e4fbb5ed6b3c0b1d84408f396d2128f43c54802b4095e196e5`
- `AetherVPN-Windows.exe`: [отчет VirusTotal](https://www.virustotal.com/gui/file/32a6ac3da3847349527580f637f2a964759ef0d89e5ae0494449db6d0987690b) | SHA-256 `32a6ac3da3847349527580f637f2a964759ef0d89e5ae0494449db6d0987690b`

### Почему на неподписанном Windows-файле возможны эвристические срабатывания на VirusTotal

На неподписанных Go-бинарниках (например, в предыдущей сборке v2.1.1 было 2/71: `Symantec` и `Bkav Pro`, при чистых Microsoft Defender, Kaspersky, ESET-NOD32, Bitdefender, Dr.Web и Google) периодически срабатывает ML-эвристика:

1. У бинарника пока нет платной цифровой подписи EV Code Signing, поэтому свежий исполняемый файл с нулевой историей скачиваний автоматически получает повышенный эвристический скор в ML-моделях (это же вызывает предупреждение Windows SmartScreen).
2. Клиент собран на Go с флагами сжатия и удаления отладочных символов (`-ldflags="-s -w"`), на что часть эвристических движков реагирует сама по себе.
3. Как и любой системный VPN-клиент, приложение использует драйвер виртуального сетевого адаптера (Wintun) и управляет таблицей маршрутизации Windows, что также добавляет вес в поведенческой эвристике.

Крупные антивирусы (Microsoft Defender, Kaspersky, ESET-NOD32, Bitdefender, Dr.Web, Google) угроз в файле не находят.
