# HDR UK Brand Package Interface

This project contains the default branding assets and style used in Open edX
applications.

The file structure serves as an interface to be implemented for custom
branding and theming of Open edX.

## How to use this package

Applications in Open edX are configured by default to include this
package for branding assets and theming visual style.

To use a custom brand and theme\...

1.  Fork or copy this project. Ensure that it lives in a location
    accessible to Open edX applications during asset builds. This may be
    a published git repo, npm, or local folder depending on your
    situation.
2.  Replace the assets in this project with your own logos or SASS
    theme. Match the filenames exactly. Open edX applications refer to
    these files by their filepath. Refer to the brand for edx.org at
    <https://github.com/edx/brand> for an example.

    If you are working with Design tokens and CSS varibles please follow the guide 
    [Paragon Design Tokens Compatibility](./docs/how-to/design-tokens-support.rst)

3.  Configure your Open edX instance to consume your custom brand
    package. Refer to this documentation on configuring the platform:
    https://docs.openedx.org/projects/openedx-proposals/en/latest/architectural-decisions/oep-0048-brand-customization.html
    \[TODO: Add a link to documentation on configuring in Open edX MFE
    pipelines when it exists\]
4.  Rebuild the assets and microfrontends in your Open edX instance to
    see the new brand reflected. \[TODO: Add link to relevant
    documentation when it is completed\].

## Files this package must make available

`/logo.svg`

![logo](/logo.svg)

`/logo-trademark.svg` A variant of the logo with a trademark ® or ™.
Note: This file must be present. If you don\'t have a trademark variant
of your logo, copy your regular logo and use that.

![logo](/logo-trademark.svg)

`/logo-white.svg` A variant of the logo for use on dark backgrounds

![logo](/logo-white.svg)

`/favicon.ico` A site favicon

![favicon](/favicon.ico)

`/paragon/images/card-imagecap-fallback.png` A variant of the default
fallback image for [Card.ImageCap] component.

![card-imagecap-fallback](/paragon/images/card-imagecap-fallback.png)

`/paragon/tokens/src/` The Futures theme as Paragon 23 design tokens.
`core/` holds mode-independent tokens (typography); `themes/light/` and
`themes/dark/` hold the colour tokens for each variant, mirroring Paragon's
own file layout so they merge over it at build time. The palette is
exposed as `color.futures.{indigo,aqua,cream,ink,ink-raised}` and every
other token references those. This is where a colour change goes.

`/paragon/core.scss` Fonts, the generated core variables, and the few
mode-independent layout rules that have no token (header geometry, logo
size, headings tracking). Compiled to `dist/core.css`.

`/paragon/themes/<variant>/index.css` and `custom.css` Each variant's
bundle: the token-generated CSS from `paragon/build/themes/<variant>/`
plus `custom.css`, the residual rules Paragon has no token for (MFE
markup such as the authn layout, the site header and the learning
sidebar). Rules reference `--pgn-*` variables, never literal colours.
Compiled to `dist/light.css` and `dist/dark.css`; the MFEs load them at
runtime through `PARAGON_THEME_URLS` (see tutor-hdrukfuturestheme).

`/paragon/_variables.scss`, `/paragon/_overrides.scss`, `/paragon/_dark.scss`
Deprecated Paragon 22 SASS theme, no longer compiled into the MFEs. Kept
only while hdruk-frontend-plugin-slots' SCSS and Storybook import them.
