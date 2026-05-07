# ConvR — Сборка APK через Termux

> Сборка идёт в облаке Expo (EAS) — Android SDK и Java не нужны.

---

## Быстрый старт (все команды по порядку)

```bash
# 1. Установить инструменты (один раз)
pkg update && pkg upgrade -y
pkg install -y nodejs-lts git unzip
npm install -g eas-cli

# 2. Распаковать архив
cp /sdcard/Download/convr-source.zip ~/projects/
cd ~/projects
unzip convr-source.zip
cd convr

# 3. ОБЯЗАТЕЛЬНО установить node_modules
npm install --legacy-peer-deps

# 4. Войти в Expo аккаунт (expo.dev — бесплатно)
eas login

# 5. Собрать APK
eas build --platform android --profile preview
```

На вопрос "Create EAS project?" → **Y**  
На вопрос "Generate new keystore?" → **Y**

Через 5–15 минут в терминале появится ссылка на APK.

---

## Если npm install падает с ENOMEM

```bash
npm install --legacy-peer-deps --max-old-space-size=512
```

Или через yarn:
```bash
pkg install yarn
yarn install --ignore-engines
```

---

## Частые ошибки

| Ошибка | Решение |
|---|---|
| `Failed to resolve plugin for module "expo-router"` | Не установлены node_modules — запустите `npm install --legacy-peer-deps` |
| `cli.appVersionSource is not set` | Уже исправлено в eas.json этого архива |
| `command not found: eas` | `npm install -g eas-cli` |
| `Run this command inside a project directory` | Вы не в папке `convr` — выполните `cd ~/projects/convr` |
