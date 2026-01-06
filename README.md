Example of how to produce an SVG file with text/font info using XeLaTeX, tikz, and dvisvgm.

Inspired by the discussion at https://tex.stackexchange.com/questions/51757/how-can-i-use-tikz-to-make-standalone-svg-graphics/71648#71648.

The example graphic is based on Figure 1.1 'The basic structure of a construction', from Croft, William. 2022. Morphosyntax: constructions of the world’s languages, p. 5.

I wanted to be able to use the same images for produceing both HTML and PDF output with Pandoc.

# Process

1. Run xelatex on `construction-diagram`:

```bash
xelatex -synctex=1 -interaction=nonstopmode "construction-diagram".tex
```

2. Run dvisvgm on the output from (1) with the --pdf flag:

```bash
dvisvgm --pdf construction-diagram.pdf -o construction-diagram.svg
```

3. Edit `construction-diagram.svg` to remove the font curve info in the `svg/style/defs` element and its descendents.

4. Edit `construction-diagram.svg` to change the `svg/style` element to refer to the locally installed font on my system:

```svg
<style type='text/css'>
.f0 {font-family: "Libertinus Serif";font-size:9.96px}
</style>
```   

The last two steps were to reduce the size of the file, as I had the font installed on my system, and also use it when producing PDF output with pandoc. This might cause other issues when used on a system without the font installed.
