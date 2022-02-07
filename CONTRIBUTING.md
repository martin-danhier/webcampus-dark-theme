# Contributing

This file contains useful documentation and knowledge for contributors.

If you notice a problem but don't have time to implement it, you can report it to us in an issue.

If you want to contribute, please fork and make pull requests ! Any help is appreciated.

Before the proposed changes can be merged, they must be tested against all supported website and browsers before being approved, since Stylus will update the style automatically if a newer version is added to the master branch.
Any help with these tests is appreciated (no one has access to all instances at once).

## Explanation of the code and coding guidelines

Whenever possible, we try to respect Material Design V2 guidelines.

The code is structured in *sections*. Each section has a list of URL patterns that Stylus will test against the URL of a visited page. If the URL matches, Stylus will inject the CSS into the page such that it overwrites the default one, thus providing the ability to tweak any website's appearance however we want.

To provide support for multiple instances of Moodle at once, two sections are applied for each website:
- A specific style that is only applied to a specific instance. This is useful if this instance uses a custom CSS.
- A common style that is applied to all instances. This is the main part of the style that is applied on top of Moodle's default style.

The use of SCSS also allows us to define constant variables (for colors or common spacings) and mixins (reusable CSS, for example for a button, elevation or ripple). Use those in priority. Moreover, all used colors should be declared in variables. That way, the colors stay consistent across the whole application, and can be easily tweaked.

Some variables, like the primary and secondary colors, are defined with vanilla CSS variables instead. Unlike SCSS variables, they keep their variable form in the compiled code, which means that different color themes can be defined for different websites. These themes are defined in the [themes](src/themes) directory.

Each time a change is merged in the master branch, the version number should be increased for the style to be updated on users' computers. This can be done in the [constants](src/constants.scss) file. It can be also changed in the [package.json](package.json) file, but it doesn't really matter for updates - only doing it on major releases is enough.

Feel free to ask questions if you have any !

## How to build

1. Clone the repository
2. Install dependencies with `npm install`
3. Run `npm run build` to build the `output.user.css` file. The output will show deprecation warnings for `@-moz-document`, but it is normal: that's the way Stylus works. However, you should fix any other error or warning you encounter.

Tip: you can also use a command-line tool to automatically copy the contents of the output file to the clipboard. For example, on Windows:

`npm run build && cat output.user.css | clip`

Once the contents is copied, you simply have to paste it in the Stylus edition tab.

*I'd be glad to hear if there is a way to directly send the output to Stylus without having to copy/paste it.*

## Current list of third-party dependencies and explanation

- `sass`: compiler for the SCSS source code
- `stylelint`: Linter for CSS files (good practices, enforce code style)
- `postcss`, `postcss-scss`: Provide SCSS syntax to Stylelint
- `stylelint-scss`: SCSS-specific rules for Stylelint