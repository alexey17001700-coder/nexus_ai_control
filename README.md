# Nexus AI Control

ИИ-хаб телефона: добавляешь любые ИИ (OpenAI-совместимый API), общаешься с ними и управляешь телефоном.

## Веб-версия (PWA)
https://alexey17001700-coder.github.io/nexus_ai_control/

Chrome → меню → «Установить приложение».

## APK (Android)

Собирается автоматически на GitHub Actions — Android Studio не нужна.

1. Открой вкладку **Actions** в этом репозитории.
2. Workflow **Build APK** → **Run workflow** (или просто запушь в `main`).
3. Дождись зелёной галочки (~4–6 мин).
4. Внизу страницы запуска — **Artifacts** → скачай `nexus-ai-control-apk`.
5. Внутри `app-debug.apk`. Скинь на телефон, разреши «Установка из неизвестных источников», установи.

### Что даёт APK
- Иконка и запуск как у обычного приложения, без браузера.
- Нативные модули Capacitor: вибрация, батарея, буфер обмена, геолокация, камера.
- Работает офлайн-оболочка, ключи ИИ хранятся локально на устройстве.

### Локальная сборка (если есть Android Studio)
```bash
npm install
mkdir -p www && cp index.html manifest.json icon.svg www/
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```

## Файлы
- `index.html` — всё приложение (UI + логика).
- `manifest.json`, `icon.svg` — PWA.
- `capacitor.config.json` — обёртка Android.
- `.github/workflows/android.yml` — авто-сборка APK.

## Безопасность
API-ключи ИИ **не хранятся в репозитории**. Вводятся на телефоне и лежат только в localStorage устройства.
