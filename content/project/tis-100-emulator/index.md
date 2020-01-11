+++
# Project title.
title = "TIS-100 Emulator"

# Date this page was created.
date = 2015-09-01T00:00:00

# Project summary to display on homepage.
summary = "Emulator and runtime for the TIS-100 language."

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["Web", "Emulator", "Lua"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Links (optional).
url_code = "https://github.com/Nickardson/TIS-100-Emulator"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
links = [{icon_pack = "fas", icon="globe-americas", name="Check it out", url = "http://tis100.tgratzer.com/"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = ""
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++

A web emulator for TIS-100. This fictional microprocessor has an assembly-like instruction set, and runs programs in unusual grid-based "CPU"s.

The game's puzzles are defined in a Lua script to allow for complex, sand­boxed user-defined specifications. My emulator also loads these user-defined puzzles using lua.vm.js.
