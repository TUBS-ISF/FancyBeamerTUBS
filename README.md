# Fancy Beamer Template for University Presentations

[![latest tag](https://img.shields.io/github/v/release/SEatUPB/FancyBeamer?style=for-the-badge&labelColor=white)](https://github.com/SEatUPB/FancyBeamer/releases/latest)&emsp;[![Static Badge](https://img.shields.io/badge/LaTeX-Inside-blue?style=for-the-badge&labelColor=darkorange&color=white)](https://www.latex-project.org/)

This is a beamer latex template for slides in a university context and can be adapted to various corporate designs.
The base template described here provides a set of nice features like columns with animations and nice boxes for definitions, examples, and more.

Originally, we developed this template specifically for ulm university at [SoftVarE-Group/SlideTemplate](https://github.com/SoftVarE-Group/SlideTemplate) but this version is no longer supported.
For university specific versions of this template, please refer to the [list of forks](https://github.com/SEatUPB/FancyBeamer/forks).
We encourage the format `FancyBeamer<UniversityAcronym>` for the fork names (e.g., [FancyBeamerUULM](https://github.com/sp-uulm/FancyBeamerUULM) for the university of ulm).

- [Fancy Beamer Template for University Presentations](#fancy-beamer-template-for-university-presentations)
  - [How to Use](#how-to-use)
    - [Creating a Presentation](#creating-a-presentation)
    - [Including the Template](#including-the-template)
    - [Creating a Symbolic Link](#creating-a-symbolic-link)
  - [Functionality of the Theme](#functionality-of-the-theme)
    - [Title Page](#title-page)
      - [Setting the Logos](#setting-the-logos)
    - [Changing Footer Transparency](#changing-footer-transparency)
    - [Content Overview](#content-overview)
    - [Section Frames](#section-frames)
    - [Slide Layout](#slide-layout)
      - [Old Macros for Slide Layouts](#old-macros-for-slide-layouts)
    - [Unique Slide-Numbering](#unique-slide-numbering)
    - [Color Boxes](#color-boxes)
      - [Custom Color Boxes](#custom-color-boxes)
      - [Counting Color Boxes](#counting-color-boxes)
      - [Old Macros for Boxes](#old-macros-for-boxes)
    - [Dark Mode](#dark-mode)
    - [Including Pictures](#including-pictures)
      - [Automatic Dark Mode for Pictures](#automatic-dark-mode-for-pictures)
    - [Other Functionalities](#other-functionalities)

## How to Use

If you are interested in a quickstart, have a look at our [demo-slides.tex](demo-slides/demo-slides.tex) or [empty-slides.tex](empty-slides/empty-slides.tex) files.

### Creating a Presentation

First, you need to create a new beamer presentation. For that, add

```tex
\documentclass[aspectratio=169]{beamer}
```

to your `.tex`-file. We recommend a font size of around 8pt for online presentations so you can use  `\documentclass[aspectratio=169,8pt]{beamer}`.

### Including the Template

Everything you desire(/require) is within the [`fancybeamer.sty`](fancybeamer.sty) file. To include it, add a line like `\usepackage{fancybeamer}` to your `.tex`-file. In general, LaTeX requires the (relative) path to the package, so depending on how you include the package (given that you do not install it in your local texmf tree), you might need to adjust the path:

``tex
\usepackage{path/to/fancybeamer}
``

### Creating a Symbolic Link

To use the template from another directory, you can create a symbolic link to the directory of the cloned template. The terminal-commands to create such links vary between different operating systems:

- **Windows:** `mklink /J \path\to\slides\template path\to\template`
- **Linux/macOS:** `ln -s /path/to/template /path/to/slides/template`

## Functionality of the Theme

### Title Page

To add a title frame, you can use the standard `\maketitle` command. It creates a title frame with a default picture and the information that is set by the following commands:

```latex
\title[<optional short title>]{<title>}
\subtitle[<optional short subtitle>]{<subtitle>}
\author[<optional short author>]{<long author>}
\date{<date>}
```

The title picture can be changed with an optional parameter: `\maketitle[<path-to-picture>]`. The picture's width will automatically be set to fill the frame. To move the picture up or down you can pass an additional optional parameter to set an offset: `\maketitle[<path-to-picture>][<offset>]`.

If no picture is given (`\maketitle`), a default picture is used. To create a title frame without a picture, you can use `\maketitle[]`.

To repeat the title slide you can use the command `\againtitle` at any point. It creates a copy of the last title slide with the same picture and picture-offset.

#### Setting the Logos

The title slide provides space to display logos.
The `\fancylogos` macro accepts a comma-separated list of paths to images which are then evenly spaced on the title slide:

```latex
\fancylogos{example-image-a,example-image-b,example-image-c}
```

You can use empty entries to alter the alignment. The following example aligns a single logo to the right:

```latex
\fancylogos{,example-image-a}
```

### Changing Footer Transparency

The transparency of the footer can be adjusted using the command `\settitlefootertransparency{<transparency>}`. The transparency value should be between 0 (completely transparent) and 1 (completely opaque).
For example (used before the `\maketitle`),

```latex 
\settitlefootertransparency{0.3}
```

will set the transparency of the logo footer to 30%.

### Content Overview

A slide that shows a clickable multi-column table of contents (including the sections and subsections of the document) can be generated using the command `\contentoverview`. The command supports an optional argument which reflects the number of columns to use. For example, `\contentoverview[2]` will make use of columns.

### Section Frames

At the begin of each section a title slide is automatically generated. If you are in handout-mode, this slide also includes an overview of all sections and subsections that can be used to navigate through the slides easily.

You can overwrite this behaviour by using one of the following options within the `\documentclass`-command (or when loading the package):

* `nosectionframes`: no automatic frames at the begin of each section
* `sectiontitleslides`: automatic title frames at the begin of each section
* `sectionoverviews`: automatic section overviews at the begin of each section


### Slide Layout

You can use the the `fancycolumns` environment to layout your slides (it is safe to use with verbatim content like source code, but still requires the beamer `fragile`-option for the frame).
Within, the `\nextcolumn` can be used to separate columns, various options allow you to customize the appearance:

```latex
\begin{fancycolumns}[columns=3, t]
   Content of Column 1
\nextcolumn
   Content of Column 2
\nextcolumn
   Content of Column 3
\end{fancycolumns}
```

In total, there are the following options:

| Option | Default | Description |
|:-------|:--------|:------------|
|`c`     | yes | Will center the content of the columns vertically |
|`t`     | no  | Will vertically align based on the baseline of the first line of each column |
|`b`     | no  | Will vertically align based on the baseline of the last line of each column |
|`T`     | no  | Similar to `t` but will use the very top of the first line (good for images, ...). |
| `width=<width>` | `\linewidth` | The total width of all columns (including margins) |
| `height=<width>` | `no height` | The artificial height of the columns environment (e.g. for animations with different heights). |
| `no height` |  | Counterpart of `height =<width>` makes the layout use the natural height again. |
| `margin=<width>` | `0.035\linewidth` | The horizontal space between columns. |
| `columns=<amount>` | `2` | The number of columns |
| `widths={<widths>}` | `{}` | A comma-separated list of values, which determine how wide the columns should be. For example, using `columns=4, widths={40,30}` will cause the first column to occupy 40% of the width, the next one 30%, and evenly distribute the remaining 30% among the other two columns (equivalent to `columns=4, widths={40,30,15,15}`). |
| `animation=none` | yes | Similar to the "and" mode of the old layouts. Will make all slides visible by default, without any animation (should not be combined with `reverse`). |
| `keep` or `animation=keep`| no | Similar to the "then" mode of the old layouts. This will cause the columns to be animated one after the other, with previous columns remaining visible. |
| `forget` or `animation=forget`| no | Similar to the "or" mode of the old layouts. This will cause the columns to be animated one after the other, with previous columns disappearing again. This behavior is active *only in recording mode* (`\recordingtrue`), otherwise, this is similar to `animation=keep`. |
| `reverse`| no | With the default animation order being left-to-right, this makes it right-to-left. |
| `extra/columns=<value>`| `{}` | Only for people who know, what they are doing. This allows direct, overwriting access on the beamer-`columns` mechanism working behind the scenes. |

Some of these defaults may appear arbitrary. They can be changed (locally to the current group) with the macro `\setfancycolumnsdefault` (accumulative):

```latex
\setfancycolumnsdefault{margin=7mm,t}
```

#### Old Macros for Slide Layouts

Please note that, all of the macros in this section are deprecated (for not being verbatim-safe). Please use the [`fancycolumns`](#slide-layout) environment described above.

The following layouts can be used to arrange content into multiple columns on a frame. Some of them are also animated.

- `\leftandright{<left>}{<right>}`, `\leftmiddleandright{<left>}{<middle>}{<right>}` <br> Splits the frame into multiple columns, which contain the content given by the multiple arguments.
- `\leftthenright{<left>}{<right>}`, `\leftmiddlethenright{<left>}{<middle>}{<right>}` <br> Splits the frame into multiple columns, which contain the content given by the multiple arguments and are displayed column by column with the previous columns remaining on the slide (only if not in `handout`-mode).
- `\leftorright{<left>}{<right>}`, `\leftmiddleorright{<left>}{<middle>}{<right>}` <br> Splits the frame into multiple columns, which contain the content given by the multiple arguments and are displayed column by column individually with a blank frame in between (only if not in `handout`-mode). <br> **Hint:** This only works if the recording mode is enabled via `\recordingtrue`, otherwise it will act the same as `\leftthenright` or `\leftmiddlethenright`.


### Unique Slide-Numbering

With the package option `uniqueslidenumber` you can ensure that even frames with overlays get a unique slide number at the bottom right.
For this, this option adds a suffix to the slide number (`<slide>.<overlay>`) of slides with animations, so the slides can be uniquely identified.

### Color Boxes

The following colored boxes can be used for writing definitions, examples and notes:

```latex
\begin{definition}{<Title>}
   <Content>
\end{definition}

\begin{example}{<Title>}
   <Content>
\end{example}

\begin{info}{<Title>}
   <Content>
\end{info}
```

#### Custom Color Boxes

You can also create own colorbox-environments with `\MakeNewBox{<box-name>}{<box-color>}` or modify existing ones using `\UpdateBoxColor{<box-name>}{<new-box-color>}`.

#### Counting Color Boxes

The prefix and suffix of a box title can be updated using `\UpdateBoxPrefix{<box-name>}{<new-prefix>}` and `\UpdateBoxSuffix{<box-name>}{<new-suffix>}` (or `\UpdateBoxSurround{<box-name>}{<new-prefix>}{<new-suffix>}`). To create a counting box, `\boxnumber` can be used in the definition of the prefix or suffix. The following example causes definitions to be numbered with a "Definition" prefix and a colon:

```latex
\UpdateBoxPrefix{definition}{Definition~\boxnumber: }%
```

You can also directly add a prefix and suffix to the box title at creation using additional options: `\MakeNewBox[<prefix>]{<box-name>}{<box-color>}[<suffix>]`.

#### Old Macros for Boxes

Please note that, all of the macros in this section are deprecated (for not being verbatim-safe). Please use the `definition`, `example` and `info` environments described above. Yet, they are still created for backwards compatibility:

- `\mydefinition{<title>}{<content>}`
- `\myexample{<title>}{<content>}`
- `\myinfo{<title>}{<content>}`

### Dark Mode

For easier viewing and editing slides in dark environments, the template features a dark mode that can be enabled with the option `darkmode` when loading the package (or in the `\documentclass` command).

### Including Pictures

Pictures can be included using the `\pic{<path>}`-command. This command also enables creating automatic links on the pictures (e.g. for sources). Therefore, the link simply has to be stored in a `.txt`-file with the same filename.

#### Automatic Dark Mode for Pictures

Similar to the `\pic` command described above, `\picDark{<path>}` can be used to include pictures that get inverted automatically when the dark mode is used. Therefore, white gets converted to a dark gray that matches the dark background color of the slides.

Alternatively, a separate dark version of the picture can be stored with the suffix `-dark` to get automatically used instead of the normal version when dark mode is enabled.

### Other Functionalities

- **Easy Navigation in Slides**\
  A click on the title or subtitle in the slide footer leads to a jump to the title slide. A click on the section title brings you to the begin of the section.
- **Auto-Scaling**\
  Frame titles that are longer than the width of the frame are scaled down automatically. This can avoid annoying linebreaks for a single character or word.
- **Recording mode**\
  This theme comes with a optional recording mode. In this mode, the animations for the content layouts `\leftorright` and `\leftmiddleorright` are different. Each column that is generated by those layouts is displayed individually one after another with a blank slide in between. That way, the presenter can walk over to the other side of the frame if recording in front of the slides. <br> The recording mode can be enabled using the command `\recordingtrue`.
- **Using Lectures**\
  Standard LaTeX `\lecture`s can also be used with the template. [`lecture-demo`](./lecture-demo) contains an example for how to use them.
