---
layout: cover
title: WebAssembly in the JavaScript Ecosystem
highlighter: shiki
colorSchema: dark
download: https://github.com/natemoo-re/slides/raw/main/2022-05-24/2022-05-24-wasm-chicago.pdf
---

<div class="flex gap-8 px-10 justify-center scale-120 transform">

<img height="222" width="111" src="/logo.svg" class="h-32" />

<div class="flex-col items-center pr-32">

<h1><div class="text-4xl mt-2">WebAssembly in the<br>JavaScript Ecosystem</div></h1>

<p text="lg" class="!leading-8 !opacity-50 !-mt-4" font="italic serif light">
Unlocking new possibilities with hybrid tooling
</p>
</div>

</div>

<div class="abs-br mx-10 my-8 flex">
  <div class="ml-3 flex flex-col text-right gap-1">
    <div class="text-md opacity-30">WebAssembly Chicago</div>
    <div class="text-sm opacity-50">May 24, 2022</div>
  </div>
</div>

---
layout: 'intro'
---

<h1 text="!5xl">Nate Moore</h1>

<div class="leading-8 opacity-80">
Astro co-creator and core team member.<br>
Creator of Microsite, TokenCSS, and many other open source projects.<br>
Senior Software Engineer at <a href="https://astro.build" target="_blank">The Astro Technology Company</a>.<br>
</div>

<div class="my-10 grid grid-cols-[40px,1fr] w-max gap-y-4">
  <ri-github-line class="opacity-50"/>
  <div><a href="https://github.com/natemoo-re" target="_blank">natemoo-re</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://twitter.com/n_moore" target="_blank">n_moore</a></div>
  <ri-user-3-line class="opacity-50"/>
  <div><a href="https://nmoo.dev" target="_blank">nmoo.dev</a></div>
</div>

<img src="/me.jpeg" class="rounded-full w-40 abs-tr mt-30 mr-20"/>

---

# The Third Age of JavaScript [^1]

JavaScript grows from a site scripting toy language to full application platform

<div class="h-90">

<v-clicks>

- Faster tooling
- ESM first
- Single tools that do many things well
- Typesafe
- More secure
- Polyglot (Native, but increasingly **WebAssembly**)

</v-clicks>

</div>

[^1]: As described by [@swyx](https://www.swyx.io/js-third-age/#the-third-age)

---

# The Third Age of JavaScript [^1]

JavaScript grows from a site scripting toy language to full application platform

<div class="h-90">

<img src="/esbuild.svg" class="w-full">

</div>

[^1]: As described by [@swyx](https://www.swyx.io/js-third-age/#the-third-age)

---
layout: center
class: text-center
---

# WebAssembly: The JavaScript Killer<span class="text-transparent">?</span>

<p class="text-transparent">&ldquo;The reports of my death are greatly exaggerated.&rdquo;</p>

---
layout: center
class: text-center
---

# WebAssembly: The JavaScript Killer?

<p>&ldquo;The reports of my death are greatly exaggerated.&rdquo;</p>

---

# WebAssembly + JavaScript
Name a more iconic duo!

<blockquote class="!p-4" v-click>
<p class="text-2xl !leading-8 py-2 mr-32">
  WebAssembly is a different language from JavaScript, but it is not intended as a replacement. 
  
  Instead, it is designed to complement and work alongside JavaScript, allowing web developers to take advantage of both languages' strong points.
</p>

– WebAssembly Concepts, [MDN](https://developer.mozilla.org/en-US/docs/WebAssembly/Concepts)

</blockquote>

---

# WebAssembly + JavaScript
Name a more iconic duo!

<div class="grid grid-cols-2 mt-8 mb-16">
<div>

## JS

- High-level
- No compilation
- Flexible, expressive
- Ecosystem

</div>
<div v-click>

## Wasm

- Low-level
- Compile target
- Near-native performance
- Portable

</div>
</div>

---

<h1>&ldquo;Hybrid&rdquo; Tooling</h1>

Takes full advantage of both JavaScript and WebAssembly's strengths

<div class="grid grid-cols-2 mt-8 mb-16">
<div>

## Traits

<v-clicks>

- JavaScript/TypeScript module on surface
- Seamless integration with Node/Deno ecosystem
- Offers high-level, user-friendly APIs
- Low barrier to entry

</v-clicks>

</div>
<div>

<h2 class="text-transparent">Traits</h2>

<v-clicks>

- WebAssembly powers low-level, internal APIs
- Focus on compute-heavy tasks (parsing, compiling)
- Delivers near-native performance

</v-clicks>

</div>
</div>

---

<h1>&ldquo;Hybrid&rdquo; Tooling</h1>

Takes full advantage of both JavaScript and WebAssembly's strengths

<div class="grid grid-cols-2 mt-8 mb-16">
<div>

## Benefits

<v-clicks>

- Built on web standards
- Compile a single `.wasm` file
- Shared data primitives
- Fully portable (Node, Deno, Browsers)
- Bridge ecosystem gaps

</v-clicks>

</div>
<div>

## Tradeoffs

<v-clicks>

- New workflow, out of comfort zone
- Immature tooling
- Performance, `near-native != native`
- Context-switching for 3 languages
- Maintenance cost, harder to contribute

</v-clicks>

</div>
</div>

---
layout: center
class: text-center
---

# Examples

---

<Example name="esbuild" description="An extremely fast JavaScript bundler" url="https://esbuild.github.io/" />

<img v-click src="/esbuild.svg" class="w-full" />

<v-clicks>

- Written in Go
- Includes JS and CSS parsers and compilers, fully featured JS bundler
- Powers next-gen build tools like [Vite](https://vitejs.dev/)
- Native bindings for Node and Deno, `.wasm` bindings for the web (automatic in [StackBlitz](https://stackblitz.com/))

</v-clicks>

<div class="mt-4" />

<v-clicks>

> The WebAssembly version is much, much slower than the native version. In many cases it is an order of magnitude (i.e. 10x) slower. This is for various reasons including a) node re-compiles the WebAssembly code from scratch on every run, b) Go's WebAssembly compilation approach is single-threaded, and c) node has WebAssembly bugs that can delay the exiting of the process by many seconds.

</v-clicks>

---

<div class="p-8 flex justify-center items-center">
  <img src="/esbuild-meme.png" class="h-100 transform scale-120" />
</div>

---

<Example name="es-module-lexer" description="Low-overhead lexer dedicated to ES module parsing for fast analysis" url="https://github.com/guybedford/es-module-lexer" />

<v-clicks>


```js
import { init, parse } from 'es-module-lexer';

await init;

const [imports, exports] = parse(`
  import { name } from "mod";
  export const data = { a: 0 };
`);
```

</v-clicks>

<div class="mt-8" />

<v-clicks>

- Written in C
- Spec-compliant JavaScript lexer
- Extracts static `import` statements, `export` statements, and dynamic `import()` usage
- Claims speed of about **5ms per MB**

</v-clicks>

<div class="mt-8" />

<v-clicks>

> Angular 1 (720KiB) is fully parsed in 5ms, in comparison to the fastest JS parser, Acorn which takes over 100ms.

</v-clicks>

---

<Example name="shiki" description="A beautiful Syntax Highlighter" url="https://shiki.matsu.io/" />

<v-clicks>

```js
import shiki from 'shiki';

const highlighter = await shiki.getHighlighter({ theme: 'github-dark' });
const code = highlighter.codeToHtml(/* source */, { lang: 'js' });
```

</v-clicks>

<div class="mt-8" />

<v-clicks>

- High-level JS library, but dependency is written in C
- First JavaScript syntax highlighter with editor-level fidelity (matches [Visual Studio Code](https://code.visualstudio.com/))
- Works with TextMate grammars and Code themes
- Powered by [`vscode-oniguruma`](https://github.com/microsoft/vscode-oniguruma), WebAssembly bindings for [`oniguruma`](https://github.com/kkos/oniguruma) RegExp library

</v-clicks>

---

<Example name="goldmark" description="A very fast Markdown compiler for Deno" url="https://deno.land/x/goldmark" />

<v-clicks>

```ts
import { init, transform } from "https://deno.land/x/goldmark/mod.ts";

await init();
const markdown = await Deno.readTextFile(new URL('./content.md', import.meta.url));
const { frontmatter, content } = await transform(markdown, /* opts */);
```

</v-clicks>

<div class="mt-8" />

<v-clicks>

- Written in Go
- WebAssembly bindings for [Goldmark](https://github.com/yuin/goldmark), a CommonMark-compliant Markdown parser
- Original package powers [Hugo](https://gohugo.io/)
- Deno's adherence to web platform spec makes working with WebAssembly easy

</v-clicks>

<div class="mt-8" />

<v-clicks>

> Sampling **100,000 runs** completed in **58s** with an average run of **0.57ms** per file.

</v-clicks>

---

<Example name="@parcel/css" description="A CSS parser, transformer, and minifier written in Rust" url="https://github.com/parcel-bundler/parcel-css" />

<div class="grid grid-cols-2 mt-4 mb-16 gap-4">
<div v-click><strong class="block mb-2">Input</strong>

```css
@custom-media --modern (color), (hover);

.foo {
  background: yellow;

  -webkit-border-radius: 2px;
  border-radius: 2px;
  -webkit-transition: background 200ms;
  transition: background 200ms;

  &.bar {
    color: green;
  }
}

@media (--modern) and (width > 1024px) {
  .a {
    color: green;
  }
}
```

</div>
<div v-click><strong class="block mb-2">Output</strong>

```css
.foo {
  background: #ff0;
  border-radius: 2px;
  transition: background 0.2s;
}
.foo.bar {
  color: green;
}
@media ((color) or (hover)) and (min-width: 1024px) {
  .a {
    color: green;
  }
}
```
</div>
</div>

---

<Example name="@parcel/css" description="A CSS parser, transformer, and minifier written in Rust" url="https://github.com/parcel-bundler/parcel-css" />

- Written in Rust

<v-clicks>

- Lowers modern CSS syntax to be compatible with configurable browser targets
- **Browser-grade** CSS parser, powered by Mozilla's own [`cssparser`](https://github.com/servo/rust-cssparser) and [`selectors`](https://github.com/servo/servo/tree/master/components/selectors) crates

</v-clicks>

<div class="mt-8" />

<img v-click src="/parcelcss.png" class="w-full" />

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

**Astro DSL**

```astro {all|2,7,13|3,12|4|9|15-19|all}
---
import Layout from '../components/Layout.astro';
import Counter from '../components/Layout.tsx'; // or vue, svelte, etc
const { items } = await fetch('https://service.dev/api/v1/items').then(res => res.json());
---

<Layout title="Items">
  <ul>
    {items.map(item => <li>{item}</li>)}
  </ul>

  <Counter slot="footer" client:idle />
</Layout>

<style>
  ul {
    color: red;
  }
</style>
```

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

- High-level JS library, but compiler is written in Go

<v-clicks>

- Features custom `.astro` DSL for building server-side websites
- Truly Hybrid: leverages WebAssembly for compute-heavy tasks, everything else is JavaScript
- Why Go?
  - Iteration speed
  - Proximity to `esbuild`
  - Superset of HTML, leverage Go's `std` library
- Ability to communicate between JS <=> Wasm

</v-clicks>

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

**JavaScript**

```js {all|4-7}
import { transform } from '@astrojs/compiler';

const result = await transform(`...`, {
  async preprocessStyle(value, attributes) {
    const newValue = await compileSass(value);
    return newValue;
  }
});
```

**Go**

```go {all|4}
func preprocessStyle(i int, style *astro.Node, transformOptions transform.TransformOptions, cb func()) {
	defer cb()
	attrs := wasm_utils.GetAttrs(style)
	data, _ := wasm_utils.Await(transformOptions.PreprocessStyle.(js.Value).Invoke(style.FirstChild.Data, attrs))
	return data[0].Get("code").String()
}
```

---
layout: center
class: "text-center"
---

# WebAssembly doesn't replace JavaScript

<h2 v-click class="opacity-50">Use the best tool (from any ecosystem) for the job</h2>

---
layout: center
class: "text-center"
---

# Thank you!

Slides can be found at [nmoo.dev/slides](https://nmoo.dev/slides)
