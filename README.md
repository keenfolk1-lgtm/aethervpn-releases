# AetherVPN

<p align="center">
  <img src="assets/logo.png" alt="AetherVPN" width="120" />
</p>

Клиент AetherVPN для Android и Windows. В этом репозитории публикуются готовые сборки и контрольные суммы SHA-256, исходный код закрыт.

## Скачать (v2.1.1)

Актуальные файлы лежат в разделе [Releases](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest):

- [AetherVPN-Android.apk](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest/download/AetherVPN-Android.apk) (Android, ARM64 и x86_64)
- [AetherVPN-Windows.exe](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest/download/AetherVPN-Windows.exe) (Windows 10/11 x64)
- [SHA256SUMS.txt](https://github.com/keenfolk1-lgtm/aethervpn-releases/releases/latest/download/SHA256SUMS.txt)

Доступ и ссылка подписки выдаются в Telegram-боте [@AetherAccessBot](https://t.me/AetherAccessBot) (есть бесплатный тест на 24 часа, дальше 100 ₽/мес). Вопросы по работе и оплате можно писать в поддержку [@maximka_sem](https://t.me/maximka_sem).

## Как подключиться

### Android

1. Скачайте `AetherVPN-Android.apk` и установите приложение.
2. Скопируйте ссылку подписки в [@AetherAccessBot](https://t.me/AetherAccessBot).
3. В приложении откройте раздел импорта, вставьте ссылку и нажмите кнопку подключения.

### Windows

1. Скачайте `AetherVPN-Windows.exe` и запустите от имени администратора (права нужны для системного TUN-интерфейса).
2. Если Windows SmartScreen покажет предупреждение о неизвестном издателе, нажмите "Подробнее", затем "Выполнить в любом случае". Предупреждение появляется из-за того, что сборка пока без платной цифровой подписи.
3. Вставьте ссылку подписки из [@AetherAccessBot](https://t.me/AetherAccessBot) и подключитесь.

## Особенности работы

Приложение использует собственный протокол Aether с маскировкой под TLS 1.3 и гибридным обменом ключами X25519 + ML-KEM. При обрыве или ограничении скорости на одном канале клиент переключается на резервный транспорт.

Российские банки, Госуслуги и локальные сайты открываются напрямую через раздельный туннель, отключать VPN для них не нужно. Список серверов обновляется внутри приложения кнопкой обновления подписки.

## Проверка файлов и VirusTotal

После скачивания сверьте SHA-256 с файлом `SHA256SUMS.txt`:

```powershell
Get-FileHash .\AetherVPN-Windows.exe -Algorithm SHA256
```

Хеши сборки v2.1.1 и страницы проверки на VirusTotal:

- `AetherVPN-Android.apk`: `c0576efa796e22e4fbb5ed6b3c0b1d84408f396d2128f43c54802b4095e196e5` ([VirusTotal](https://www.virustotal.com/gui/file/c0576efa796e22e4fbb5ed6b3c0b1d84408f396d2128f43c54802b4095e196e5))
- `AetherVPN-Windows.exe`: `09e1a9c97ba05b6e7443b9983910bb0de268a6d4fd069f0ce9d6dc373deb7839` ([VirusTotal](https://www.virustotal.com/gui/file/09e1a9c97ba05b6e7443b9983910bb0de268a6d4fd069f0ce9d6dc373deb7839))
