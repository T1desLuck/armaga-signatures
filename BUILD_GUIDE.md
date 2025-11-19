# Armaga - Руководство по сборке

## 📋 Требования

### Обязательные:
- **Android Studio** Hedgehog (2023.1.1) или новее
- **JDK 17** или новее
- **Android SDK 36** (compileSdk)
- **Минимум Android SDK 21** (Android 5.0)
- **Kotlin 2.0.21+**
- **Gradle 8.7+**

### Рекомендуемые:
- 8 GB RAM минимум (16 GB рекомендуется)
- 10 GB свободного места на диске
- Эмулятор Android или физическое устройство

## 🚀 Быстрый старт

### 1. Клонирование проекта
```bash
cd c:\flutter_projects\armaga_kotlin
```

### 2. Синхронизация Gradle
```bash
gradlew.bat --refresh-dependencies
```

### 3. Сборка Debug версии
```bash
gradlew.bat assembleDebug
```

### 4. Установка на устройство
```bash
gradlew.bat installDebug
```

## 📦 Сборка Release версии

### 1. Создание keystore (первый раз)
```bash
keytool -genkey -v -keystore armaga-release.keystore -alias armaga -keyalg RSA -keysize 2048 -validity 10000
```

### 2. Настройка signing config
Создайте файл `keystore.properties` в корне проекта:
```properties
storePassword=your_store_password
keyPassword=your_key_password
keyAlias=armaga
storeFile=armaga-release.keystore
```

### 3. Сборка Release APK
```bash
gradlew.bat assembleRelease
```

APK будет в: `app/build/outputs/apk/release/app-release.apk`

## 🔧 Решение проблем

### Ошибка: "SDK location not found"
Создайте `local.properties`:
```properties
sdk.dir=C\:\\Users\\YourUsername\\AppData\\Local\\Android\\Sdk
```

### Ошибка: "Execution failed for task ':app:kspDebugKotlin'"
```bash
gradlew.bat clean
gradlew.bat assembleDebug
```

### Ошибка: "Out of memory"
Увеличьте heap в `gradle.properties`:
```properties
org.gradle.jvmargs=-Xmx4096m -Dfile.encoding=UTF-8
```

### Ошибка: "Manifest merger failed"
Проверьте `AndroidManifest.xml` на конфликты

## 📱 Запуск на эмуляторе

### Создание эмулятора через Android Studio:
1. Tools → Device Manager
2. Create Device
3. Выберите Pixel 6 или новее
4. Выберите API 36 (Android 16) или API 34 (Android 14)
5. Finish

### Запуск через командную строку:
```bash
gradlew.bat installDebug
adb shell am start -n com.armaga.antivirus/.MainActivity
```

## 🧪 Тестирование

### Unit тесты:
```bash
gradlew.bat test
```

### Instrumentation тесты:
```bash
gradlew.bat connectedAndroidTest
```

### Lint проверка:
```bash
gradlew.bat lint
```

## 📊 Анализ сборки

### Размер APK:
```bash
gradlew.bat assembleRelease
dir app\build\outputs\apk\release
```

### Анализ зависимостей:
```bash
gradlew.bat app:dependencies
```

### Build scan:
```bash
gradlew.bat assembleDebug --scan
```

## 🔍 Отладка

### Логи приложения:
```bash
adb logcat | findstr "Armaga"
```

### Очистка данных:
```bash
adb shell pm clear com.armaga.antivirus
```

### Проверка разрешений:
```bash
adb shell dumpsys package com.armaga.antivirus
```

## 📝 Полезные команды

### Список устройств:
```bash
adb devices
```

### Установка APK:
```bash
adb install app\build\outputs\apk\debug\app-debug.apk
```

### Удаление приложения:
```bash
adb uninstall com.armaga.antivirus
```

### Скриншот:
```bash
adb shell screencap -p /sdcard/screen.png
adb pull /sdcard/screen.png
```

## 🎯 Оптимизация сборки

### Включение кэша:
```properties
org.gradle.caching=true
org.gradle.parallel=true
org.gradle.configureondemand=true
```

### Использование Gradle Daemon:
```bash
gradlew.bat --daemon
```

### Очистка кэша:
```bash
gradlew.bat clean cleanBuildCache
```

## 📚 Дополнительные ресурсы

- [Android Developer Guide](https://developer.android.com/guide)
- [Jetpack Compose Documentation](https://developer.android.com/jetpack/compose)
- [Hilt Documentation](https://dagger.dev/hilt/)
- [Room Database Guide](https://developer.android.com/training/data-storage/room)

## ⚠️ Важные замечания

1. **Первая сборка** может занять 5-10 минут
2. **Gradle sync** должен завершиться без ошибок
3. **Все зависимости** загружаются автоматически
4. **Минимальная версия Android** - 5.0 (API 21)
5. **Целевая версия** - Android 16 (API 36)

## 🐛 Известные проблемы

### Windows Defender может блокировать Gradle
Добавьте папку проекта в исключения

### Антивирус может замедлять сборку
Временно отключите или добавьте в исключения

### Проблемы с кодировкой
Убедитесь что `gradle.properties` содержит:
```properties
org.gradle.jvmargs=-Dfile.encoding=UTF-8
```

## 📞 Поддержка

При возникновении проблем:
1. Проверьте логи: `gradlew.bat assembleDebug --stacktrace`
2. Очистите проект: `gradlew.bat clean`
3. Invalidate Caches в Android Studio
4. Проверьте версии SDK и JDK

---

**Успешной сборки! 🚀**
