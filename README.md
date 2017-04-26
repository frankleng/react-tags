# React Tag Autocomplete

[![Build status](https://api.travis-ci.org/i-like-robots/react-tags.svg?branch=master)](https://travis-ci.org/i-like-robots/react-tags) [![Coverage Status](https://coveralls.io/repos/github/i-like-robots/react-tags/badge.svg?branch=master)](https://coveralls.io/github/i-like-robots/react-tags)

React Tag Autocomplete is a simple tagging component ready to drop in your React projects. Originally based on the [React Tags project](http://prakhar.me/react-tags/example) by Prakhar Srivastav this version removes the drag-and-drop re-ordering functionality, adds appropriate roles and ARIA states and introduces a resizing text input. React Tag Autocomplete is compatible with [Preact](https://preactjs.com/) >= 6.0.0.

![React Tags Autocomplete](https://dl.dropboxusercontent.com/u/2664340/ReactTags.png)

## Installation

The preferred way of using the component is via NPM

```
npm install --save react-tag-autocomplete
```

## Usage

Here's a sample implementation that initializes the component with a list of preselected `tags` and a `suggestions` list. For more details, go through the [API](#Options).

```js
var ReactTags = require('react-tag-autocomplete');

var App = React.createClass({
  getInitialState: function () {
    return {
      tags: [
        { id: 1, name: "Apples" },
        { id: 2, name: "Pears" }
      ],
      suggestions: [
        { id: 3, name: "Bananas" },
        { id: 4, name: "Mangos" },
        { id: 5, name: "Lemons" },
        { id: 6, name: "Apricots" }
      ]
    }
  },
  handleDelete: function (i) {
    var tags = this.state.tags.slice(0)
    tags.splice(i, 1)
    this.setState({ tags: tags })
  },
  handleAddition: function (tag) {
    var tags = this.state.tags.concat(tag)
    this.setState({ tags: tags })
  },
  render: function () {
    return (
      <ReactTags
        tags={this.state.tags}
        suggestions={this.state.suggestions}
        handleDelete={this.handleDelete}
        handleAddition={this.handleAddition} />
    )
  }
})

React.render(<App />, document.getElementById('app'))
```

### Options

- [`tags`](#tagsOption)
- [`suggestions`](#suggestionsOption)
- [`placeholder`](#placeholderOption)
- [`autofocus`](#autofocusOption)
- [`autoresize`](#autoresizeOption)
- [`minQueryLength`](#minQueryLengthOption)
- [`maxSuggestionsLength`](#maxSuggestionsLengthOption)
- [`classNames`](#classNamesOption)
- [`handleAddition`](#handleAdditionOption)
- [`handleDelete`](#handleDeleteOption)
- [`handleInputChange`](#handleInputChange)
- [`allowNew`](#allowNew)
- [`tagComponent`](#tagComponent)

<a name="tagsOption"></a>
#### tags (optional)

An array of tags that are displayed as pre-selected. Each tag must have an `id` and a `name` property. Default: `[]`.

```js
var tags =  [
  { id: 1, name: "Apples" },
  { id: 2, name: "Pears" }
]
```

<a name="suggestionsOption"></a>
#### suggestions (optional)

An array of suggestions that are used as basis for showing suggestions. Each suggestion must have an `id` and a `name` property and an optional `disabled` property. Default: `[]`.

```js
var suggestions = [
  { id: 3, name: "Bananas" },
  { id: 4, name: "Mangos" },
  { id: 5, name: "Lemons" },
  { id: 6, name: "Apricots", disabled: true }
]
```

<a name="placeholderOption"></a>
#### placeholder (optional)

The placeholder string shown for the input. Default: `'Add new tag'`.

<a name="autofocusOption"></a>
#### autofocus (optional)

Boolean parameter to control whether the text-input should be autofocused on mount. Default: `true`.

<a name="autoresizeOption"></a>
#### autoresize (optional)

Boolean parameter to control whether the text-input should be automatically resized to fit its value. Default: `true`.

<a name="minQueryLengthOption"></a>
#### minQueryLength (optional)

How many characters are needed for suggestions to appear. Default: `2`.

<a name="maxSuggestionsLengthOption"></a>
#### maxSuggestionsLength (optional)

Maximum number of suggestions to display. Default: `6`.

<a name="classNamesOption"></a>
#### classNames (optional)

Override the default class names. Defaults:

```js
{
  root: 'react-tags',
  rootFocused: 'is-focused',
  selected: 'react-tags__selected',
  selectedTag: 'react-tags__selected-tag',
  selectedTagName: 'react-tags__selected-tag-name',
  search: 'react-tags__search',
  searchInput: 'react-tags__search-input',
  suggestions: 'react-tags__suggestions',
  suggestionActive: 'is-active',
  suggestionDisabled: 'is-disabled'
}
```

<a name="handleAdditionOption"></a>
#### handleAddition (required)

Function called when the user wants to add a tag. Receives the tag.

```js
function (tag) {
  // Add the tag { id, name } to the tag list
  tags.push(tag)
}
```

<a name="handleDeleteOption"></a>
#### handleDelete (required)

Function called when the user wants to delete a tag. Receives the tag index.

```js
function (i) {
  // Delete the tag at index i
  tags.splice(i, 1)
}
```

<a name="handleInputChange"></a>
#### handleInputChange (optional)

Optional event handler when the input changes. Receives the current input value.

```js
function (input) {
  if (!this.state.busy) {
    this.setState({ busy: true })

    return fetch(`query=${input}`).then(function (result) {
      this.setState({ busy: false })
    })
  }
}
```

<a name="allowNew"></a>
#### allowNew (optional)

Allows users to add new (not suggested) tags. Default: `false`.

<a name="allowBackspace"></a>
#### allowBackspace (optional)

Disables ability to delete the selected tags when backspace is pressed while focussed on the text input. Default: `true`.

<a name="tagComponent"></a>
#### tagComponent (optional)

Provide a custom tag component to render. Default: `null`.

### Styling

It is possible to customize the look of the component the way you want it. An example can be found in `/example/styles.css`.

### Development

The component is written in ES6 and uses [Webpack](http://webpack.github.io/) as its build tool.

```
npm install
npm run dev # open http://localhost:8080
```

### Upgrading from 4.x to 5.x

1. The `delimiters` option has been removed, any references to this will now be ignored.
2. The `classNames` option has been updated:

  ```udiff
  {
  -  root: 'ReactTags',
  -  tagInput: 'ReactTags__tagInput',
  -  selected: 'ReactTags__selected',
  -  tag: 'ReactTags__tag',
  -  tagName: 'ReactTags__tagName',
  -  suggestions: 'ReactTags__suggestions',
  -  isActive: 'is-active',
  -  isDisabled: 'is-disabled'
  +  root: 'react-tags',
  +  rootFocused: 'is-focused',
  +  selected: 'react-tags__selected',
  +  selectedTag: 'react-tags__selected-tag',
  +  selectedTagName: 'react-tags__selected-tag-name',
  +  search: 'react-tags__search',
  +  searchInput: 'react-tags__search-input',
  +  suggestions: 'react-tags__suggestions',
  +  suggestionActive: 'is-active',
  +  suggestionDisabled: 'is-disabled'
  }
  ```

For smaller changes refer to [the changelog](CHANGELOG.md).
