Welcome to the *RECON learn* project
====================================

This github project hosts the sources of the
[RECON](http://www.repidemicsconsortium.org/) learn platform, live at:
<https://reconlearn.netlify.com/>.

This *RECON learn* website uses
[Rmarkdown](http://rmarkdown.rstudio.com/) (`.Rmd`) documents to build
markdown content that [Hugo](https://gohugo.io) then turns into a nifty
website.

General workflow
----------------

The general workflow would include the following steps:

1.  **Fork the project** from the github *RECON learn* project:

This will create a copy of the project in your own github account. You
will need to clone this archive, and make the modifications there. You
`git clone` would look like:

``` bash
git clone https://github.com/johnsnow/learn
```

If your github user name is `johnsnow`.

1.  **Add new content**, typically in the form of a new `.Rmd` file and
    associated media (most often images). Regular posts such as
    practicals, tutorials, and case studies are stored in
    `content/post/`. Other content which is not rendered as typical html
    reports such as lecture slides can be stored in `static`.

2.  **Generate content** by using the `R/render_new_rmds_to_md.R`
    script, to build the `.md` files and associated graphics.

3.  `git commit` and `git push` all changes; don’t forget to add new
    images as well (run `git status` to see which files haven’t been
    added).

4.  Make a **pull request** against the main project (`master` branch),
    from the github *RECON learn* project:

Make sure you use `reconhub/learn`, branch `master` as base fork:

Contributing content
--------------------

Practicals, tuorials, case studies are contributed as
[Rmarkdown](http://rmarkdown.rstudio.com/) (`.Rmd`) documents and
generated markdown ready for conversion as `.md` documents. They are
stored in `content/post`. The best way to create a new document is
copy-paste an existing one and rename it.

### Conventions

Naming conventions are as follows:

-   start with `practical` for practicals, `study` for case studies
-   use lower case, no special characters
-   be hypen-separated (“-”)

For instance, for a practical using a SEIR model for influenza data:

-   `practical-seir-influenza` is good
-   `SEIR-flu` is bad as lacking ‘practical’ (it could be a lecture),
    and has capitalised letters
-   `practical-new` is bad, as it is non-informative

### Editing the YAML header

The YAML header is the beginning of the `Rmd` document, within the
`---`. For instance:

``` r
---
title: Phylogenetic tree reconstruction
author: Thibaut Jombart
categories: ["practicals"]
topics: ["genetics"]
date: 2017-11-01
image: img/highres/trees.jpg
showonlyimage: true
bibliography: practical-phylogenetics.bib
licenses: CC-BY
---
```

Fields are mostly self-explanatory, and can be adapted to your needs.
The date should respect the format provided.

### Storing images

The **image** will be the image associated with the document on the
website. We try using natural, high-resolution, evocative images having
a link, if only figurative, with the topic covered. These images are
stored in `static/img/highres/`. Do not forget to add and push this file
as well, as it will be required for your post to be successfully
integrated. The path to the file provided in the header assumes
`static/` as root folder (see example above), so that the right path
will look like: `img/highres/your-image.jpg`.

### Bibliographies

The **`bibliography`** is optional. If provided, it should contain
references cited in the document as a `bibtex` file (`.bib`). Do not
forget to add and push this file as well, as it will be required for
your post to be successfully integrated.

Contributing slides
-------------------

Material for slides is stored in `static/slides`. Currently, two files
are needed for a lecture:

1.  a `.Rmd` post in `content/post` (see above) to introduce the lecture
    and link to the slides; for an example, look at
    `content/post/lecture-reproducibility.Rmd`.

2.  the slides themselves, stored in `static/slides`.

For the slides, we recommended using `.Rmd` there again, and rendering
them before committing them. If your slides use images, store them in
`static/img/slides`. You will be able to refer to them using
`../../img/slides/your-image.jpg`. For an example of
`rmarkdown+ioslides` slides, look at
`static/slides/intro_reproducibility_Rmd/intro_reproducibility.Rmd`.

Other topics
------------

### Contributing top-level pages

To contribute a page that sits outside of the posts category you can
make an `.md` file (or a `.Rmd` file so long as you render to `.md`
too). This will then be processed by Hugo along with the other files to
build the website.

These files should have at minimum:

``` r
---
date : 2017-11-01
title : About RECON learn
---
```

### Maintaining package dependencies

This repository also has a DESCRIPTION which lists any packages required
to build all of the `.Rmd` files in `content/post/`. Keep it up to date
with `R/get_and_update_dependencies.R`. You will need `tidyverse` and
`devtools` installed for the script to run.

### Getting the dependencies

If you need to install the dependencies locally, you can use
`devtools::install()` in the console to fetch all the dependencies.

### Editing existing content

If you need to change an existing piece of content: 1. Delete its
corresponding `.md` file 2. Make the changes to the `.Rmd` file 3. Run
`R/render_new_rmds_to_md.R` 4. Commit and push to the repository
