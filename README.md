# Commands

### Epub

```bash
pandoc assets/metadata.yaml chapters/*.md -o build/book.epub
```

### MOBI

```bash
ebook-convert build/book.epub build/book.mobi
```

### PDF

```bash
pandoc assets/title.md chapters/*.md -o build/book.pdf -t html5 -S -V papersize:"letter" -c ../assets/style.css
```

### HTML

```bash
pandoc assets/metadata.yaml chapters/*.md -s --toc --no-highlight  --css ../assets/style.css -A assets/template/footer.html -o build/book.html
```

#### Notes

- Must include `language-php` in fenced code blocks.