# eBook Boilerplate

## Scripts

### `pre-process`

Convert `*` to `-language-*` for fenced code blocks for Prism.js.

```bash
#!/bin/bash -e

derived_dir=derived
rm -fr ${derived_dir} && mkdir -p ${derived_dir}
for file in $*
do
    cat ${file} | sed 's/```php/```language-php/g; s/```js/```language-js/g; s/```sql/```language-sql/g ; s/```css/```language-css/g; s/```scss/```language-scss/g; s/```html/```language-html/g' > ${derived_dir}/$(basename ${file})
done
echo "${derived_dir}/*"
```

### `chapters`

Create an HTML page for each chapter.

```bash
#!/bin/bash -e
CHAPTERS=chapters/*
TEMPLATE=assets/template/

for chapter in $CHAPTERS
do
    filename=${chapter##*/}
    html="${filename%.*}.html"
    pandoc $(pre-process $chapter) -s --no-highlight  --css ../assets/css/style.css -B $TEMPLATE/header.html -A $TEMPLATE/footer.html -o web/$html
done
```

## Commands

### Epub

```bash
pandoc assets/metadata.yaml  --css assets/css/style-epub.css chapters/*.md --highlight-style assets/new-moon.theme -o build/book.epub
```

### MOBI

```bash
ebook-convert build/book.epub build/book.mobi
```

### PDF

```bash
pandoc assets/title.md chapters/*.md -o build/book.pdf -t html5 -S -V papersize:"letter" -c ../assets/css/style.css
```

### HTML

```bash
chapters
```

Example:

```
pandoc chapters/01-chapter.md -s --no-highlight --css ../assets/css/style.css -B assets/template/header.html -A assets/template/footer.html -o web/chapter1.html
```

## Needs

- Pagination
- Book cover
- Example theme
- Filenames