<h1 align="center">vue-timestamp</h1>

<p align="center">
<a href="https://www.npmjs.com/package/vue-timestamp"><img src="https://img.shields.io/npm/v/vue-timestamp.svg"/> <img src="https://img.shields.io/npm/dm/vue-timestamp.svg"/></a> <a href="https://vuejs.org/"><img src="https://img.shields.io/badge/vue-2.x-brightgreen.svg"/></a>
</p>

> A simple "x days ago" component for Vue, using the html `time` tag.

# Project goals:
1. Be as lightweight as possible
2. Use HTML `time` tags

The basics of this package come from [this gist](https://gist.github.com/mage3k/e4b0eb24d4a19b28f4f24aee8a194107).

# CSS

There is no included CSS, but you may use the `.time` class for styling.

This is totally personal preference, but I like the look of the following:

```css
.time {
  margin-left: .5em;
  font-weight: normal;
  font-style: italic;
}
```

This looks pretty good next to user names and such.

# Props

| Name                           | Type     | Default        | Description         |
|--------------------------------|----------|----------------|--------------------------------------------------------------|
| `date`                         | Date     | `new Date()`   | A JS `Date` object of the time you wish to represent. |
| `interval`                     | Number   | `5000`         | How often *in milliseconds* to update the timestamp. |
| `timeLimit`                    | Number   | `3600`         | If the difference between `date` and the current time is greater then `timeLimit` (*in seconds*), polling will not occur in order to save computation time. |
