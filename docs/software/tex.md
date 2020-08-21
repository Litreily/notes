# Tex

## install texlive & tex2pdf

* install texlive `sudo apt-get install texlive`
* install tex2pdf https://sourceforge.net/projects/tex2pdf.berlios/

``` bash
sudo mv tex2pdf /usr/bin
tex2pdf --configure
tex2pdf <filename>.tex
```

there may remind you that not found `subfloat.sty`

## install subfloat.sty

* download `subfloat.sty` https://ctan.org/tex-archive/macros/latex/contrib/subfloat
* unzip this .zip file

``` bash
cd subfloat
./install.sh
```

``` bash
$ kpsewhich -var-value=TEXMFHOME
/home/litreily/texmf
$ sudo mkdir -p ~/texmf/subfloat
$ cp subfloat.sty ~/texmf/subfloat/
$ sudo texhash
```

or

``` bash
sudo cp subfloat.sty /usr/share/latex/subfloat/
# or
sudo cp subfloat.sty /usr/share/texlive/texmf-dist/tex/latex/subfloat/

sudo texhash
```

* check subfloat.sty

``` bash
$ kpsewhich subfloat.sty
/usr/share/texmf/tex/latex/subfloat/subfloat.sty
```
