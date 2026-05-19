---
title: Branding Handbook
abstract: A guide to the visual identity and design language of felixweber.co.uk, including typography, colour palette, gradients, text shadows, borders, buttons, spacing, and design principles.
author: Felix Weber
date: 2026-05-19
toc: true
---

\chapter{Branding Handbook}

# Branding Handbook

This handbook documents the visual identity and design language for felixweber.co.uk.

# Typography

## Typefaces

| Role                     | Typeface       | Format    |
| ------------------------ | -------------- | --------- |
| Display/Headings/Buttons | **PixChicago** | TTF, WOFF |
| Body/UI Text             | **w95fa**      | WOFF2     |
| Fallback                 | `sans-serif`   | System    |

**PixChicago** is a pixel-style bitmap font evoking classic Mac OS Chicago. It is used exclusively for all headings (H1–H6), buttons, and any interactive UI labels to reinforce the retro identity.

**w95fa** is a Windows 95-inspired proportional font used for all body text and prose. Its familiar, slightly chunky letterforms complement PixChicago without competing with it.

## Type Scale

| Element              | Size      | Notes                              |
| -------------------- | --------- | ---------------------------------- |
| Hero H1 (header)     | 2.5em     | Gradient + text-shadow, PixChicago |
| H1 (content)         | 2em       | Pink shadow offset                 |
| H2                   | 1.5em     | Cyan shadow offset                 |
| H3                   | 1em       | No shadow                          |
| H2 (header subtitle) | 1.2em     | Centred                            |
| Body                 | 16px base | w95fa, line-spacing 1.2            |
| Buttons/`.btn`       | 0.8em     | PixChicago, no underline           |

## Text Styling Rules

- **Line height** for headings and buttons: `1.2`
- **Line spacing** for body: `1.2`
- **Links**: Underline appears on hover only
- **Buttons**: `text-decoration: none` always; underline suppressed
- **Text alignment**: All headings within `header` are **centred**

# Colour Palette

The palette blends a soft lavender background with neutral content surfaces and two signature wide-gamut neon accent colours. Where supported, Display P3 colour values are used over sRGB fallbacks for more vivid reproduction.

## Base Colours

| Name                      | Hex/Value | Usage                                      |
| ------------------------- | --------- | ------------------------------------------ |
| **Page Background**       | `#faf0fa` | `<body>` background – soft lavender white  |
| **Page Background (alt)** | `#f0fafa` | `<body>` background – soft baby blue white |
| **Surface/Card**          | `#f6f6f6` | Sections, header, main – light neutral     |
| **Foreground/Text**       | `#333333` | Primary body text, HR borders              |
| **Mobile Background**     | `#f6f6f6` | Body background on screens ≤ 600px         |

## Button Colours

| State                        | Colour                                   |
| ---------------------------- | ---------------------------------------- |
| Default                      | `#d3d3d3` (light grey)                   |
| Hover                        | `#c0c0c0` (silver)                       |
| Active/Pressed               | `#a9a9a9` (dark grey)                    |
| Readability Button (default) | `rgba(228, 173, 255, 1)` – soft lavender |
| Readability Button (pressed) | `rgba(181, 105, 212, 1)` – medium purple |

## Accent Colours (Neon)

| Name             | sRGB Fallback             | Display P3                          | Usage                          |
| ---------------- | ------------------------- | ----------------------------------- | ------------------------------ |
| **Neon Magenta** | `rgba(251, 8, 255, 0.64)` | `color(display-p3 1 0.0039 1)`      | H1 text-shadow, gradient start |
| **Neon Cyan**    | `rgba(8, 218, 255, 0.64)` | `color(display-p3 0.0039 0.8549 1)` | H2 text-shadow, gradient end   |

Declare the sRGB `rgba()` value first, then the `color(display-p3 …)` override. Browsers that support Display P3 will use the richer value; others fall back gracefully.

# Gradients

## Hero Title Gradient

Used on the `<header> <h1>` element as a clipping gradient to colour the text.

```
Direction:    45deg
Start colour: color(display-p3 1 0.0039 1)       [Neon Magenta]
End colour:   color(display-p3 0.0039 0.8549 1)  [Neon Cyan]
Background-size: 40% 100%
Background-position: center
Animation:    gradient – 10s ease infinite
```

The gradient is applied using `background-clip: text` and `-webkit-text-fill-colour: transparent`. This makes the gradient text appear like the shadow of the bold black text to the user. However, technically, the dark drop-shadow created with `4px 4px 0 colour(display-p3 0 0 0.2)` is actually the shadow of the gradient text even though it looks like the main bold black text.

**sRGB:**

```css
background: linear-gradient(
  45deg,
  rgba(251, 8, 255, 0.64),
  rgba(8, 218, 255, 0.64)
);
```

**Display P3:**

```css
background: linear-gradient(
  45deg,
  color(display-p3 1 0.0039 1),
  color(display-p3 0.0039 0.8549 1)
);
```

# Text Shadows

## H1 (Content Sections)

An offset pink pixel shadow evokes retro chromatic aberration.

```css
text-shadow: -1px 1px 0 rgba(251, 8, 255, 0.64);
text-shadow: -1px 1px 0 color(display-p3 1 0.0039 1);
```

## H2 (Content Sections)

A matching cyan offset shadow.

```css
text-shadow: -1px 1px 0 rgba(8, 218, 255, 0.64);
text-shadow: -1px 1px 0 color(display-p3 0.0039 0.8549 1);
```

## Hero H1 Drop Shadow

```css
text-shadow: 4px 4px 0 rgba(0, 0, 0, 0.3);
text-shadow: 4px 4px 0 color(display-p3 0 0 0.2);
```

# Borders & Surfaces

## Pixel-Corner Border

Cards (`header`, `main`, `section`) use an SVG pixel-corner border image to simulate a chunky retro frame.

```css
border: 15px solid transparent;
border-image: url("pixel-corner.svg") 20 round;
border-radius: 20px;
```

- **Border width:** 15px
- **Border-image slice:** 20
- **Border-image repeat:** `round`
- **Border-radius:** 20px (rounded corners under the border image)
- **Mobile override (≤ 600px):** Border removed entirely; `border: 0; border-image: none; border-radius: 0`

## Divider

> `<hr>`

```css
border: none;
border-top: 4px dotted #333;
margin: 20px 0;
```

A 4px dotted line in foreground colour. Within lists, the **final** `<hr>` is hidden (`display: none`).

## Post Header Title

```css
border-bottom: 4px dotted #333;
```

Matching dotted underline applied below `.post-header > h1`.

# Buttons

## Base Button

> `.btn`

```css
background-color: #d3d3d3;
color: #000;
padding: 10px 15px;
border: 2px solid #000;
border-radius: 5px;
font-family: "PixChicago", sans-serif;
font-size: 0.8em;
box-shadow:
  inset 0 2px 0 rgba(255, 255, 255, 0.5),
  inset 0 -2px 0 rgba(0, 0, 0, 0.5);
transition:
  background-color 120ms ease,
  transform 120ms ease,
  box-shadow 120ms ease;
```

The double inset shadow creates a bevelled/raised appearance consistent with the Windows 95 aesthetic.

## Button States

<!--prettier-ignore-->
| State               | Background     | Box-Shadow                                                            | Transform         |
| ------------------- | -------------- | --------------------------------------------------------------------- | ----------------- |
| Default             | `#d3d3d3`      | `inset 0 2px 0 rgba(255,255,255,0.5), inset 0 -2px 0 rgba(0,0,0,0.5)` | –                 |
| Hover               | `#c0c0c0`      | Same as default                                                       | –                 |
| Active/Pressed      | `#a9a9a9`      | `inset 0 -3px 0 rgba(9,8,8,0.6)`                                      | `translateY(2px)` |

Pressed state uses `aria-pressed="true"` for accessibility. The `translateY(2px)` shift and reversed shadow simulate a physical button depression.

## Readability Button

> `#readability-btn`

A special accent button using the lavender-purple palette.

| State   | Background               |
| ------- | ------------------------ |
| Default | `rgba(228, 173, 255, 1)` |
| Pressed | `rgba(181, 105, 212, 1)` |

The readability button toggles pixel-style body fonts on and off; when depressed, the body text changes to a sans-serif font.

# Spacing & Layout

## Page Layout

| Property                     | Value                      |
| ---------------------------- | -------------------------- |
| Body padding                 | `20px`                     |
| Body margin                  | `20px`                     |
| Max content width            | `900px`                    |
| Content horizontal alignment | `margin: 0 auto` (centred) |
| Card margin-bottom           | `20px`                     |

## Card Inner Spacing

- Border of 15px (creates visual inset padding via border-image)
- No explicit inner padding defined on cards; content relies on child element padding

## Row/Flex Layout

```css
display: flex;
flex-wrap: wrap;
justify-content: space-evenly;
align-items: center;
padding: 10px;
gap: 10px;
```

Used for arranging multiple items (links, buttons, images) horizontally with even distribution and wrapping on smaller screens.

## Heading Spacing

```css
margin: 10px;
padding-bottom: 15px;
text-align: center; /* header context */
```

## Mobile Breakpoint

> ≤ 600px

| Property           | Change                           |
| ------------------ | -------------------------------- |
| Body background    | `#f6f6f6` (matches card surface) |
| Body padding       | `10px`                           |
| Body margin        | `10px`                           |
| Card border        | Removed                          |
| Card border-radius | `0`                              |

# Images

```css
img {
  max-width: 100%;
  height: auto;
}
```

All images are fully responsive, scaling down within their container without distortion.

# Design Principles

1. Wide-gamut where possible, and always provide an sRGB fallback before the `color(display-p3 …)` declaration. The neon accents exist beyond the sRGB gamut – on P3 displays they appear noticeably more vivid.
1. Interactive elements (e.g. buttons) use a greyscale palette (silver → grey progression) so that neon text colours and the readability button's lavender always read as accent elements.
1. Buttons must use `aria-pressed` to communicate toggle state both visually (transform + shadow inversion) and semantically. Accessibility is a first-class requirement.

\chapter{Files}

# LaTeX

A `felixweber.latex` file defines the pandoc-LaTeX template for PDF generation in line with the felixweber.co.uk identity.
