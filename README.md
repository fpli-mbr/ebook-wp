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
pandoc assets/metadata.yaml $(pre-process chapters/*.md) -s --toc --no-highlight  --css ../assets/style.css -B assets/template/header.html -A assets/template/footer.html -o build/book.html
```

#### Notes

Must use `pre-process` script:

```bash
#!/bin/bash -e

derived_dir=derived
rm -fr ${derived_dir} && mkdir -p ${derived_dir}
for file in $*
do
    cat ${file} | sed 's/```php/```language-php/g' > ${derived_dir}/$(basename ${file})
done
echo "${derived_dir}/*"
```