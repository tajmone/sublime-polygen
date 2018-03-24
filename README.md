# Sublime Polygen

"__Polygen__" package for __Sublime Text 3__.

https://github.com/tajmone/sublime-polygen

Adds syntax highlighting for Polygen grammars (`*.grm`), useful editing features like Goto symbol functionality, a grammars info snippet and a variety of build systems for testing, checking and preprocessing grammar files directly in the editor. Ships with two dedicated color schemes.

- Polygen syntax: Polygen Meta Language (PML) 1.0
- Build system: Polygen v1.0.6

-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="true" lowercase_only_ascii="true" uri_encoding="true" depth="3" -->

- [Requirements](#requirements)
- [Installation](#installation)
- [Features](#features)
    - [Syntax Highlighting](#syntax-highlighting)
    - [Color Schemes](#color-schemes)
        - [Polygen Glamour](#polygen-glamour)
        - [Polygen Monokai](#polygen-monokai)
    - [Goto Symbol](#goto-symbol)
    - [Build Systems](#build-systems)
    - [Grammar Info Snippet](#grammar-info-snippet)
        - [Custom Variables Support](#custom-variables-support)
- [License](#license)
- [Contributing](#contributing)
- [Features Requests and Support](#features-requests-and-support)

<!-- /MarkdownTOC -->

-----

# Requirements

Requires __Sublime Text 3__ BUILD `>=3149`.

Build systems require Polygen tool to be on the system PATH in order to work.

# Installation

Install via "__Package Control__: Install Package", search for package "__Polygen__" and let Package Control install it for you, so it will be automatically updated when required.

For manual installation (not recommended), create a "`Polygen`" folder inside "`<data_path>/Packages/`", open a shell inside "`<data_path>/Packages/Polygen/`" and type:

```
git clone https://github.com/tajmone/sublime-polygen .
```

Don't forget the "`.`" after the repository URL! it's needed in order to clone the repository contents directly into the current folder, without creating a "`sublime-polygen`" container folder.

# Features

- [Syntax highlighting]
- [Custom color schemes]
- [Goto non-terminal or labels]
- [Build and test systems]
- [Grammar info snippet]

## Syntax Highlighting

Sublime Polygen provides robust support for Polygen grammars syntax, with nice syntax highlighting capable of distinguishing:

- non-terminal symbols in rule definition
- non-terminal symbols in productions
- labels
- labels in dot selections (grouped or isolated)
- keyword operators
- probability operators
- strings
- escape sequences in strings
- Ascii escape sequences in strings
- invalid Ascii escape sequences in strings
- comments

Each of the above listed items provides a specific scope, allowing to implement different syntax coloring in custom color schemes.

Non-terminal symbols in rule definition and in productions both share a common scope, but the former as an additional scope allowing to (optionally) implement a different highlighting style for symbols in rule definitions (e.g., in bold). Similarly, labels and labels in dot selections share a common scope, but the former has an additional scope. These additional scopes for non-terminals and lables are also used by the Goto symbol functionality, in order to quickly find non-terminal symbols only in definition rules, and navigate labels occurences by skipping label selections.

> __NOTE__ — Polygen syntax is defined using ST3's new `.sublime-syntax` file format, added in __BUILD 3103__ (2016-02-09).

## Color Schemes

Because of the nature of Polygen Meta Language (PML), the syntax uses some custom (and rather arbitrary) scope names, and therefore ships with two dedicated color schemes conceived for better syntax highlighting results.

The package ships with two color schemes:

- "Polygen Glamour" (default)
- "Polygen Monokai"

Neither of them will be enforced by the package installation; enabling them is up to the user and can be achieved by editing the User settings file for Polygen syntax.

To enable a color scheme, open the menu:

    Preferences > Package Settings > Polygen > Settings

this will launch a new instance of Sublime Text, with the default settings of Sublime Polygen in the left pane, and the file "`<data_path>/Packages/User/Polygen.sublime-settings`" in the right pane. Edit the JSON User settings file (on the right) as required to add the following key-value pair:

```json
{
    "color_scheme": "Packages/Polygen/Polygen-Glamour.sublime-color-scheme"
}
```

... where `Polygen-Glamour.sublime-color-scheme` should be the name of the desired scheme (change it to `Polygen-Monokai.sublime-color-scheme` if you want to use the Monokai scheme).

In the left pane you'll find comment-out example settings and guidelines which you can copy and paste over to the right pane; these include notes and presets for the color schemes.


> __NOTE__ — Both color schemes are defined using ST3's new `.sublime-color-scheme` format, added in __DEV BUILD 3149__ (2017-10-13).

### Polygen Glamour

"Polygen Glamour" is the default scheme. It's dark and warm, with a vintage color palette. 

![Polygen Glamour][Screenshot Glamour]


```json
{
    "color_scheme": "Packages/Polygen/Polygen-Glamour.sublime-color-scheme"
}
```

### Polygen Monokai

"Polygen Monokai" is the alternative scheme. Based on Sublime Text's native "Monokai" scheme, by Wimer Hazenberg, and adapted to Polygen's syntax scopes in order to provide better color balance among the syntax elements.

![Polygen Monokai][Screenshot Monokai]

```json
{
    "color_scheme": "Packages/Polygen/Polygen-Monokai.sublime-color-scheme"
}
```


## Goto Symbol

Sublime Polygen implements Goto Symbol functionality to allow quickly finding non-terminals and labels in long grammars. Only non-terminal symbols in rule definitions and non-selection labels are indexed, on a per-file basis.

This should reflect the common usage scenario, where one wants to quickly find a non-terminal definition rule, or all the occurences of a label inside productions (but not in dot selections).

"Goto Definition" and "Goto Reference" are not supported because grammars are treated as isolated files, so that Goto Symbol functionality is confined to the current file only (ignoring other grammars open in the editor, or inside the project).


## Build Systems

Sublime Polygen offers a variety of build and test systems that can be accessed from any "`*.grm`" source file via the `Tools > Build` and `Tools > Build With…` menus (or via <kbd>Ctr</kbd> <kbd>B</kbd> and <kbd>Ctr</kbd> <kbd>Shift</kbd> <kbd>B</kbd>, respectively). 

![Build Systems][Screenshot Build Systems]

The build functionality requires Polygen tool to be on the system PATH.

The default build system (<kbd>Ctr</kbd> <kbd>B</kbd>) will run the current grammar with Polygen and show the result in Sublime Text's console.

The "Build With…" menu (or <kbd>Ctr</kbd> <kbd>Shift</kbd> <kbd>B</kbd>) will bring up more choices:

- `Polygen`
- `Polygen - verbose`
- `Polygen - build to file (<filename>.out.txt)`
- `Polygen - build to file verbose`
- `Polygen - check grammar`
- `Polygen - check grammar (pedantic)`
- `Polygen - show grammar info`
- `Polygen - preprocess`
- `Polygen - preprocess to file (<filename>.pre.txt)`

where, unless `to file` is specified, all operations' output is printed to ST console. File operations will direct Polygen output to a file in the source grammar's folder, following the name convention specified within brackets.

The above build systems represent common testing operations while working on a grammar source code, and they allow to perform these tests without leaving the editor. For big grammars with long output, the `to file` variants of these operations can be used, and the output file kept open in Sublime Text, so that with each execution of the build system the contents of the output file will be refreshed in the editor, allowing to test a grammar's output live in the editor.

## Grammar Info Snippet

The Info snippet provides a quick template for adding the description block to a grammar:

![Grammar Info Snippet][Screenshot info snippet]

By typing "`info`"+<kbd>Tab</kbd> inside a "`*.grm`" file, you'll get:

``` polygen
I ::=   "title:    \n"
      ^ "author:   \n"
      ^ "language: \n"
      ^ "status:   embryonic\n"
      ^ "topic:    \n"
      ^ "audience: \n"
      ^ "disclaim: \n"
      ^ "created:  DD/MM/YY\n"
;
```

with the cursor positioned after the `title` field, and you can then <kbd>Tab</kbd> your way through to the next fields.

The `I` non-terminal symbol is used by Polygen to provide a summary string about the grammar, via the `-info` command line option. The actual format of the string is not strictly defined, rather it's a convention amongst Polygen users. The `info` snippet generates a preset based on common practices found in most grammars, and provides a sample value for `status` and a placeholder reminder of the date format commonly used for the `created` field (`DD/MM/YY`).

You are free to add your custom fields, and omit fields which you don't need. You can also copy the "`Polygen/snippets/info.sublime-snippet`" file in "`Packages/User/`" and adapt it to your custom needs.

### Custom Variables Support

The `info` snippets also supports custom environment variables as default values for some of its fields:

![Grammar Info Snippet Vars][Screenshot info env vars]

The supported variables are:

- `POLYGEN_AUTHOR`
- `POLYGEN_LANG`

When these environment variable are defined, their values will automatically be used to fill the `author` and `language` fields, respectively.

To define these environment variables, create a "`Polygen_Env_Vars.tmPreferences`" file (the actual filename doesn't really matter, only the extension) in "`Packages/User/`", and define them like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>name</key>
    <string>Custom Polygen env vars</string>
    <key>scope</key>
    <string>source.polygen</string>
    <key>settings</key>
    <dict>
        <key>shellVariables</key>
        <array>
            <dict>
                <key>name</key>
                <string>POLYGEN_AUTHOR</string>
                <key>value</key>
                <string>Tristano</string>
            </dict>
            <dict>
                <key>name</key>
                <string>POLYGEN_LANG</string>
                <key>value</key>
                <string>Italian</string>
            </dict>
        </array>
    </dict>
</dict>
</plist>
```

After creating this file, the `info` snippet will automatically fill-in the `author` and `language` fields with your custom variables:

```xml
I ::=   "title:    \n"
      ^ "author:   Tristano\n"
      ^ "language: Italian\n"
      ^ "status:   embryonic\n"
      ^ "topic:    \n"
      ^ "audience: \n"
      ^ "disclaim: \n"
      ^ "created:  DD/MM/YY\n"
;
```

# License

"__Sublime Polygen__" was created by Tristano Ajmone and released under the terms of the MIT License:

    MIT License

    Sublime Polygen
    Copyright (c) 2018 Tristano Ajmone
    https://github.com/tajmone/sublime-polygen

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.


# Contributing

Contributions are welcome via pull requests on GitHub:

- https://github.com/tajmone/sublime-polygen

# Features Requests and Support

If you have a feature request, need support or wish to report bugs, please open an Issue at:

- https://github.com/tajmone/sublime-polygen/issues



[Syntax highlighting]: #syntax-highlighting
[Custom color schemes]: #color-schemes
[Goto non-terminal or labels]: #goto-symbol
[Build and test systems]: #build-systems
[Grammar info snippet]: #grammar-info-snippet

[Screenshot Glamour]: https://raw.github.com/tajmone/sublime-polygen/master/screenshots/color-scheme-glamour.gif "'Polygen Glamour' color scheme screenshot"
[Screenshot Monokai]: https://raw.github.com/tajmone/sublime-polygen/master/screenshots/color-scheme-monokai.gif "'Polygen Monokai' color scheme screenshot"
[Screenshot Build Systems]: https://raw.github.com/tajmone/sublime-polygen/master/screenshots/build-systems.gif "Preview of Polygen build systems"
[Screenshot info snippet]: https://raw.github.com/tajmone/sublime-polygen/master/screenshots/info-snippet.gif
[Screenshot info env vars]: https://raw.github.com/tajmone/sublime-polygen/master/screenshots/info-snippet-vars.gif
