# openScale-mini-pro

Тестовая сборка openScale для PICOOC Mini Pro (Bluetooth-имя `PICOOC-CQ`).

## Скачать APK

[**Скачать APK (85 МБ)**](https://github.com/NIK-TOTO/openScale-mini-pro/releases/download/picooc-mini-pro-test-2/openScale-debug.apk) · [Страница релиза](https://github.com/NIK-TOTO/openScale-mini-pro/releases/tag/picooc-mini-pro-test-2)

Сборка и выбранные тесты успешно прошли в GitHub Actions. Скачивание APK, его контрольная сумма и подпись проверены. [Журнал сборки](https://github.com/NIK-TOTO/openScale-mini-pro/actions/runs/40773470173).

Пакет `com.health.openscale.debug` устанавливается рядом с OSS. Создайте профиль с правильными полом, ростом и возрастом, выберите PICOOC-CQ и проверьте два взвешивания с переподключением. Это изменённая тестовая сборка, не официальный релиз openScale.

## Изменения и проверка

Поддерживается 13-байтовый пакет `0x39`: вес и импеданс сохраняются через стандартную модель openScale, состав тела рассчитывает существующая `StandardImpedanceLib`. Локально прошли 68 выбранных тестов, включая 6 новых для Mini Pro; тот же набор запускается перед публикацией APK. Проверка с реальными весами ещё не проводилась.

[Подробный отчёт](REPORT.ru.md) · [Патч](openScale-picooc-mini-pro.patch) · [Рецепт сборки](.github/workflows/build-apk.yml)

## Исходный код и лицензия

GPL-3.0-or-later, см. [LICENSE](LICENSE). Полный исходный код: [oliexdev/openScale, commit 87edad4813e400cd4871109fc72a0bcf4d13f336](https://github.com/oliexdev/openScale/tree/87edad4813e400cd4871109fc72a0bcf4d13f336) плюс [прилагаемый патч](openScale-picooc-mini-pro.patch).

Для самостоятельной сборки примените патч к указанному commit и выполните в `android_app` команду `./gradlew :app:assembleDebug`. Нужны JDK 21 и Android SDK Platform 37. Контрольная сумма опубликованного APK находится в `SHA256SUMS` релиза.
