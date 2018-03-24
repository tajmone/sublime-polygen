# Sublime Polygen Changelog

# v1.1.0 (2018/03/24)

This update fixes some requirements for inclusion in [Package Control Default Channel], as requested by project reviewers (see [PR #6948]).

- `Polygen.sublime-settings`
    + Removed redundant file extensions settings
    + All Default Settings commented out (all settings are now just commented presets the user can refer to)
- New __Non-Terminal Definition__ snippet (`nt`)
- Updated Documentation


[fix some issues]: https://github.com/wbond/package_control_channel/pull/6948#issuecomment-374080071

# v1.0.0 (2018/02/17)

Sublime-Polygen v1.0.0 (`ST >=3149`), first GitHub release; [pull-requested] for inclusion in [Package Control Default Channel].

- Polygen syntax: PML 1.0
- Syntax highlighting
- Two color schemes (Polygen-specific):
    + "Polygen Glamour" (default)
    + "Polygen Monokai"
- __Grammar Info__ snippet (`info`)
- Goto Symbol:
    + non-terminal symbols in rule definition
    + labels (except in dot selections)
- Build Systems for Polygen v1.0.6:
    + `Polygen`
    + `Polygen - verbose`
    + `Polygen - build to file (<filename>.out.txt)`
    + `Polygen - build to file verbose`
    + `Polygen - check grammar`
    + `Polygen - check grammar (pedantic)`
    + `Polygen - show grammar info`
    + `Polygen - preprocess`
    + `Polygen - preprocess to file (<filename>.pre.txt)`


[Package Control Default Channel]: https://github.com/wbond/package_control_channel

[pull-requested]: https://github.com/wbond/package_control_channel/pull/6948

[PR #6948]: https://github.com/wbond/package_control_channel/pull/6948
