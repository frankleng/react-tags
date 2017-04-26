# Changelog

## 5.2.0

- Add `allowBackspace` option to disable the ability to delete the selected tags when backspace is pressed while focussed on the text input
- Refactors `updateInputWidth` method to update when any props change ([@joekrill](https://github.com/joekrill))

## 5.1.0

- Added `tagComponent` option to allow the rendering of a custom tag component

## 5.0.4

- Fixed cursor focus being lost when clicking a suggestion

## 5.0.3

- Fixed word boundary regex restricting suggestions to ascii characters

## 5.0.2

- Fixed unescaped queries throwing an exception when being converted to regexp

## 5.0.1

- Fixed `maxSuggestionsLength` not being passed to suggestions component

## 5.0.0

- Removed `delimiters` option
- Added support for jsnext entry point
- Removed functionality to hide suggestions list when escape is pressed
- Added functionality to hide suggestions list when input is blurred
- Added class name to component root when input is focused
- Refactored components to ES6 class syntax and stateless functions
- Refactored components to use Standard code style
- Refactored `classNames` option to better match usage and use BEM naming convention

## 4.3.1

- Fixed React semver that was too tight

## 4.3.0

- Updated to support React 15.0.0

## 4.2.0

- Added `allowNew` option
- Fixed incorrect partial matches when adding a tag

## 4.1.1

- Fixed mising index from active descendent attribute

## 4.1.0

- Added `classNames` option

## 4.0.2

- Fixed missing `type` attribute from tag buttons

## 4.0.1

- Fixed out of date dist package

## 4.0.0

- Removed `busy` option and status indicator
- Added `maxSuggestionsLength` option
