## `Intl.CounterFormat`
> ECMAScript Proposal, specs, and reference implementation for `Intl.CounterFormat`.

__Authors:__ [@Aleen](https://github.com/aleen42)

This proposal is currently drafted, and not in any stage of the [process](https://tc39.github.io/process-document/).

### Motivation

The W3C organization has introduced "**CSS Counter Styles Level 3**" in [the specification](https://www.w3.org/TR/css-counter-styles-3/), which has extended many internal counter formats related to an international format like `simp-chinese-informal`:

```html
<ol style="list-style-type: simp-chinese-informal">
  <li>one</li>
  <li>two</li>
  <li>three</li>
</ol>
```

However, when I want to simulate these custom styles with JavaScript to make it more compatible with older browsers like Internet Explorer, or anyone else, I need to depend on an external library, like [`@jsamr/counter-style`](https://github.com/jsamr/react-native-li/tree/master/packages/counter-style),  rather than an internal standard JavaScript implementation.

### Syntax

```
new Intl.NumberFormat(counterStyles)
```

#### Parameters

- `counterStyles`: to specify which standard counter styles you want to use.

#### Returns

- Returns a new object, which can be used to format an output string.

### Usage

```js
const formatter1 = new Intl.CounterFormat('decimal');
console.log(formatter1.format(1)); // => "1"

const formatter2 = new Intl.CounterFormat('lower-roman');
console.log(formatter2.format(1)); // => "i"

const formatter3 = new Intl.CounterFormat('lower-alpha');
console.log(formatter3.format(1)); // => "a"

const formatter4 = new Intl.CounterFormat('simp-chinese-informal');
console.log(formatter4.format(1)); // => "一" (U+4E00)

const formatter5 = new Intl.CounterFormat('cjk-earthly-branch');
console.log(formatter5.format(1)); // => "甲" (U+7532)

const formatter6 = new Intl.CounterFormat('lower-greek');
console.log(formatter6.format(1)); // => "α" (U+03b1)

const formatter7 = new Intl.CounterFormat('hiragana');
console.log(formatter7.format(1)); // => "あ" (U+3042)

const formatter8 = new Intl.CounterFormat('katakana');
console.log(formatter8.format(1)); // => "ア" (U+30A2)
```

### FAQ

1. What is the limited range?

   A: `[-2147483647, 2147483647]`, which has been tested via HTML:

   ```html
   <ol start="2147483647">
     <li>one</li> <!-- 2147483647. one -->
     <li>two</li> <!-- 2147483647. two -->
     <li>three</li> <!-- 2147483647. three -->
   </ol>
   ```

2. Should we consider the prefix or suffix?

   A: What we mainly need is the formatted counter string, rather than the prefix or the suffix, which can be easily joined with a string literal. It means the formatter should not output a fixed prefix or suffix like `a.`, or `一、`, but `a`, or `一`.

***Notice: If you have any suggestions or ideas about this proposal? Appreciate your discussions via issues.***
