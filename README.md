# Agent Skills Library

Общая библиотека переносимых Agent Skills.

## Установленные скиллы

| Скилл | Версия | Источник | Статус |
|---|---:|---|---|
| `video` | `0.7.1` | `guimatheus92/mcp-video-analyzer` | Зафиксирован источник и версия |
| `video-studio-pro` | `1.0.0` | Авторский синтез пяти публичных video skills | Добавлен в репозиторий |

### Video Studio Pro

Файл скилла: [`skills/video-studio-pro/SKILL.md`](skills/video-studio-pro/SKILL.md)

Метаданные: [`skills/video-studio-pro/metadata.json`](skills/video-studio-pro/metadata.json)

Источники и методика отбора: [`skills/video-studio-pro/references/SOURCES.md`](skills/video-studio-pro/references/SOURCES.md)

Возможности:

- транскрибация, кадры, OCR, метаданные и анализ таймкодов;
- пакетная обработка и поиск по видеоколлекции;
- локальный монтаж FFmpeg, субтитры, вертикальные клипы и компрессия;
- маршрутизация text/image/video-to-video генерации;
- HTML/GSAP и React/Remotion рендеринг;
- обязательная проверка готового файла через ffprobe.

Установка из библиотеки после клонирования:

```bash
npx skills add NikolaKuznec/git_clone --skill video-studio-pro
```

### Оригинальный MCP Video Analyzer

Зафиксированная версия: `0.7.1`, upstream commit `13b4dfa25399a0f5435c3396cdd810f5d9364ed6`.

```bash
npx skills add guimatheus92/mcp-video-analyzer
```

Дополнительно для YouTube, Instagram, TikTok, Vimeo и других платформ:

```bash
pip install yt-dlp
```

Рекомендуются Node.js 18+, Python 3.10+ и FFmpeg/ffprobe.
