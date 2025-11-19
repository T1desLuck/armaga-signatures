# 📦 Настройка GitHub репозитория для баз сигнатур

## 🎯 Что нужно сделать:

### 1. Создать файл `databases/metadata.json` в репозитории:

```json
{
  "version": "2024.11.19",
  "download_url": "https://raw.githubusercontent.com/T1desLuck/armaga-signatures/main/databases/signatures-v2024.11.19.zip",
  "sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
  "size": 1024,
  "updated_at": "2024-11-19T16:30:00Z",
  "signatures_count": 1000
}
```

### 2. Создать ZIP файл с базой сигнатур:

Структура ZIP файла `signatures-v2024.11.19.zip`:
```
signatures/
  ├── md5_hashes.txt
  ├── sha256_hashes.txt
  └── threat_info.json
```

**Пример `md5_hashes.txt`:**
```
d41d8cd98f00b204e9800998ecf8427e,Android.Trojan.FakeBank,CRITICAL
098f6bcd4621d373cade4e832627b4f6,Android.Adware.Generic,MEDIUM
5d41402abc4b2a76b9719d911017c592,Android.Spyware.SMS,HIGH
```

**Пример `sha256_hashes.txt`:**
```
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855,Android.Trojan.Banker,CRITICAL
```

**Пример `threat_info.json`:**
```json
{
  "threats": [
    {
      "hash": "d41d8cd98f00b204e9800998ecf8427e",
      "name": "Android.Trojan.FakeBank",
      "type": "TROJAN",
      "severity": "CRITICAL",
      "description": "Fake banking application that steals credentials",
      "first_seen": "2024-01-15"
    }
  ]
}
```

### 3. Загрузить файлы в репозиторий:

```bash
cd armaga-signatures
mkdir -p databases

# Создать metadata.json
cat > databases/metadata.json << 'EOF'
{
  "version": "2024.11.19",
  "download_url": "https://raw.githubusercontent.com/T1desLuck/armaga-signatures/main/databases/signatures-v2024.11.19.zip",
  "sha256": "CALCULATED_SHA256_HERE",
  "size": 1024,
  "updated_at": "2024-11-19T16:30:00Z",
  "signatures_count": 1000
}
EOF

# Создать ZIP файл (после создания файлов сигнатур)
zip -r databases/signatures-v2024.11.19.zip signatures/

# Рассчитать SHA256
sha256sum databases/signatures-v2024.11.19.zip

# Обновить metadata.json с правильным SHA256

# Закоммитить
git add databases/
git commit -m "Add virus signatures database v2024.11.19"
git push origin main
```

### 4. Проверить доступность:

Открыть в браузере:
- https://raw.githubusercontent.com/T1desLuck/armaga-signatures/main/databases/metadata.json
- https://raw.githubusercontent.com/T1desLuck/armaga-signatures/main/databases/signatures-v2024.11.19.zip

## 🔄 Обновление базы:

Когда нужно обновить базу:
1. Создать новый ZIP с новой версией
2. Обновить metadata.json с новой версией и SHA256
3. Закоммитить и запушить
4. Приложение автоматически скачает обновление

## ⚠️ Важно:

- **SHA256** должен быть точным! Приложение проверяет целостность файла
- **version** должна увеличиваться (формат YYYY.MM.DD или YYYY.MM.DD-HH)
- **download_url** должен указывать на raw.githubusercontent.com
- Файлы должны быть в ветке `main`
