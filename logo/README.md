# Знак Enot

Енот на бирюзовой плитке. Нарисован для проекта с нуля вектором (2026-10-05, `enot-clients#54`), лицензия — как у всего репозитория (`LICENSE`).

| Файл | Что это | Где используется |
| --- | --- | --- |
| `logo.svg` | основной знак, плитка со скруглением | интерфейс, иконка вкладки, страница макетов |
| `logo-square.svg` | квадрат без скругления, рисунок крупнее | `apple-touch-icon.png` (iOS скругляет сам) |
| `logo-maskable.svg` | квадрат, рисунок в безопасной зоне 80% | maskable-иконки манифеста PWA |

Цвета: плитка `#3FB5A0` (акцент тёмной темы), морда `#C9CED4`, маска и нос `#1E2227`, внутренняя часть ушей `#2B3036`, белые детали `#FFFFFF`. Подложка не нужна — плитка своя, знак одинаков в обеих темах.

## Растровые файлы

Растр — производные, в репозитории не хранятся: их собирают из SVG и кладут туда, откуда приложение их раздаёт (`enot-clients/apps/web/public/`).

```sh
R() { magick -background none -density 600 "$1" -resize "$2x$2" "$3"; }
R logo.svg 96 favicon-96x96.png
for s in 16 32 48; do R logo.svg $s ico$s.png; done
magick ico16.png ico32.png ico48.png favicon.ico
magick -background none -density 600 logo-square.svg -resize 180x180 \
  -background "#3FB5A0" -alpha remove -alpha off apple-touch-icon.png
R logo-maskable.svg 192 web-app-manifest-192x192.png
R logo-maskable.svg 512 web-app-manifest-512x512.png
```

Изменился знак — меняется здесь, затем копия `logo.svg` и растр обновляются в `enot-clients` и строка знака в `enot-docs/docs/ui/mockups.html`.
