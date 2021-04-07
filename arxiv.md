The arXiv system doesn't work well with the file structure I like:
```
fig/
    teaser.tex
    teaser.pdf
    model.tex
    model.pdf
    ...
sec/
    0_abs.tex
    1_intro.tex
    ...
tbl/
    ablation.tex
    baselines.tex
macros.tex
main.bib
main.tex
packages.tex
```
because it will remove `fig/*.pdf` since they all have paired `.tex` files
with the same filenames ("Hey, but the extensions are different!" I know...).

The workflow I follow is:

1. Expand all `.tex` so that we have a single, all-in-one file `main_arxiv.tex`
   (and this will also remove all comments for privacy):
    ```bash
    cd "$LATEX_PROJECT_ROOT"
    latexpand --empty-comments main.tex -o main_arxiv.tex
    ```

    `latexpand` comes with MacTeX:
    ```bash
    $ which latexpand
    /Library/TeX/texbin/latexpand
    ```

1. Remove all now-redundant files:
    ```bash
    rm -f fig/*.tex

    # Remove all .tex files except main_arxiv.tex
    mv main_arxiv.tex fig/
    rm -f *.tex
    mv fig/main_arxiv.tex ./

    rm -rf sec/
    rm -rf tbl/
    ```

1. Compress PDFs to make sure the final .zip will be less than 50 MB:
    ```bash
    PDF_FILE='fig/big.pdf'
    gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dNOPAUSE -dQUIET -dBATCH -sOutputFile="$PDF_FILE".compressed "$PDF_FILE"
    mv "$PDF_FILE".compressed "$PDF_FILE"
    ```
   If the compressed quality is not ideal, see
   [`unix.md`](https://github.com/xiumingzhang/cheatsheets/blob/master/unix.md)
   for other compression options available.

1. Make sure the project still compiles into the correct PDF by doing `latex`,
   `bibtex`, `latex`, and again `latex` in TeXShop. Also click "Trash Aux Files."

1. Remove the compiled PDF (because it's big) to stay under 50 MB.
