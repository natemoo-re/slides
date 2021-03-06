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

<!-- 
- Loved Brian's talk at the last meetup, reached out about presenting
- Really appreciate working with Dan to make this happen


- Look at WebAssembly specifically in JS/TS ecosystems
- Focus on Node + Deno, that's what I'm into 
- Wasm's potential for building tools that would have been previously impossible
- Get into concept of "hybrid" tooling and look at some exciting examples
-->

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
  <div><a href="https://nmoo.dev/on/github" target="_blank">natemoo-re</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://nmoo.dev/on/twitter" target="_blank">n_moore</a></div>
  <ri-user-3-line class="opacity-50"/>
  <div><a href="https://nmoo.dev" target="_blank">nmoo.dev</a></div>
</div>

<img src="/me.jpeg" class="rounded-full w-40 abs-tr mt-30 mr-20"/>

<!-- 
- Co-creator of Astro, does many things, but it's a new tool for building websites on the server and shipping minimal client-side JS
  - I'm a core maintainer, great team of folks, enthusiastic community
  - Was technical lead on Astro compiler, started my interest in WebAssembly
- I've worked on a bunch of smaller open-source projects
- Work at Astro Tech Co, same team behind Snowpack and Skypack
  - Now we're focused on supporting Astro, building community up 
-->

---

# The Third Age of JavaScript [^1]

JavaScript grows from a site scripting toy language to full application platform

<div class="h-90">

<v-click>

- Faster tooling
- ESM first
- Single tools that do many things well
- Typesafe
- More secure
- Polyglot (Native, but increasingly **WebAssembly**)

</v-click>

</div>

[^1]: As described by [@swyx](https://www.swyx.io/js-third-age/#the-third-age)

<!-- 
### Sets the stage for a new "changing of the guard"
- Coined by Shawn Wang
- Started in 2020
-->

---

# The Third Age of JavaScript [^1]

JavaScript grows from a site scripting toy language to full application platform

<div class="h-90">

<img src="/esbuild.svg" class="w-full">

</div>

[^1]: As described by [@swyx](https://www.swyx.io/js-third-age/#the-third-age)

<!-- 
### `esbuild` is the perfect example
- Fundamental shift for JS devs
- Push to native _for_ JS, at least for low-level tools
-->

---
layout: center
class: text-center
---

# WebAssembly: The JavaScript Killer<span class="text-transparent">?</span>

<p class="text-transparent">&ldquo;The reports of my death are greatly exaggerated.&rdquo;</p>

<!-- 
### Mostly hype, haven't seen signs yet
- Chance at a "do-over" for the web
-->

---
layout: center
class: text-center
---

# WebAssembly: The JavaScript Killer?

<p>&ldquo;The reports of my death are greatly exaggerated.&rdquo;</p>

<!-- 
### JavaScript isn't going anywhere
- Both technologies play well with each other
- Ecosystem is slowly becoming more reliant on WebAssembly
-->

---

# WebAssembly + JavaScript
Name a more iconic duo!

<blockquote class="!p-4" v-click>
<p class="text-2xl !leading-8 py-2 mr-32">
  WebAssembly is a different language from JavaScript, but it is not intended as a replacement. 
  
  Instead, it is designed to complement and work alongside JavaScript, allowing web developers to take advantage of both languages' strong points.
</p>

??? WebAssembly Concepts, [MDN](https://developer.mozilla.org/en-US/docs/WebAssembly/Concepts)

</blockquote>

<!-- 
### MDN highlights motivations behind WebAssembly
- Not a replacement, but a complement
- The takeaway being... JS is good! Wasm is good! Use the right tool for the task at hand.
-->

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


<!--
#### JS
- High-level
- Doesn't require a build step
- Dynamic language, so flexible and expressive
- Has an incredible ecosystem in Node (and increasingly Deno)

#### Wasm
- Low-level
- Usually not hand-written, but compiled to
- Great performance characteristics
- Big one for me: portable. You can take your `.wasm` anywhere (Node, Deno, browsers, other Wasm runtimes)
-->

---

<h1>&ldquo;Hybrid&rdquo; Tooling</h1>

Takes full advantage of both JavaScript and WebAssembly's strengths

<div class="grid grid-cols-2 mt-8 mb-16">
<div>

<v-click>

## Traits

- JavaScript/TypeScript module on surface
- Seamless integration with Node/Deno ecosystem
- Offers high-level, user-friendly APIs
- Low barrier to entry

</v-click>

</div>
<div>

<h2 class="text-transparent">Traits</h2>

<v-click>

- WebAssembly powers low-level, internal APIs
- Focus on compute-heavy tasks (parsing, compiling)
- Delivers near-native performance

</v-click>

</div>
</div>

<!-- 
### I've mentioned this idea of Hybrid tooling, what is it?
- Plays to both languages strengths
- Surface-level, just a JavaScript module
- Benefits of that are seamless, user-friendly APIs, and approachability

- Internally, leverages Wasm to handle internal tasks
- Focus on computationally expensive things
- Super performant, will see that this is common among examples
-->

---

<h1>&ldquo;Hybrid&rdquo; Tooling</h1>

Takes full advantage of both JavaScript and WebAssembly's strengths

<div class="grid grid-cols-2 mt-8 mb-16">
<div>

## Benefits

- Built on web standards
- Compile a single `.wasm` file
- Shared data primitives
- Fully portable (Node, Deno, Browsers)
- Bridge ecosystem gaps

</div>
<div>

<v-click>

## Tradeoffs

- New workflow, out of comfort zone
- Immature tooling
- Performance, `near-native != native`
- Context-switching for 3 languages
- Maintenance cost, harder to contribute

</v-click>

</div>
</div>

<!-- 
### Like everything, there are tradeoffs
- Good!
  - Standardized
  - portable format
  - shared primitives
  - bridge between ecosystems
- Bad!
  - Comfort zone
  - tools are young, Rust invested the most!
  - slower than native, maybe this gap will close?
  - contributors
-->


---
layout: center
class: text-center
---

# Examples

---

<Example name="esbuild" description="An extremely fast JavaScript bundler" url="https://esbuild.github.io/" />

<img v-click src="/esbuild.svg" class="w-full" />

<v-click>

- Written in Go
- Includes JS and CSS parsers and compilers, fully featured JS bundler
- Powers next-gen build tools like [Vite](https://vitejs.dev/)
- Native bindings for Node and Deno, `.wasm` bindings for the web (automatic in [StackBlitz](https://stackblitz.com/))

</v-click>

<div class="mt-4" />

<v-click>

> The WebAssembly version is much, much slower than the native version. In many cases it is an order of magnitude (i.e. 10x) slower. This is for various reasons including a) node re-compiles the WebAssembly code from scratch on every run, b) Go's WebAssembly compilation approach is single-threaded, and c) node has WebAssembly bugs that can delay the exiting of the process by many seconds.

</v-click>

<!-- 
### The big one, `esbuild`
- Written in Go
- Fully featured web stack bundler
- Being used as low-level tool in a lot of popular projects
- Does have native bindings, but used Wasm for browser
  - Big caveat, author prefers native binaries
  - Some Node and Go-specific issues that are solvable
-->

---

<div class="p-8 flex justify-center items-center">
  <img src="/esbuild-meme.png" class="h-100 transform scale-120" />
</div>

<!-- 
- The internal code `esbuild` uses to load the proper binary is incredibly complex
- Could just use a single Wasm file
-->

---

<Example name="es-module-lexer" description="Low-overhead lexer dedicated to ES module parsing for fast analysis" url="https://github.com/guybedford/es-module-lexer" />

<v-click>


```js
import { init, parse } from 'es-module-lexer';

await init;

const [imports, exports] = parse(`
  import { name } from "mod";
  export const data = { a: 0 };
`);
```

</v-click>

<div class="mt-8" />

<v-click>

- Written in C
- Spec-compliant JavaScript lexer
- Extracts static `import` statements, `export` statements, and dynamic `import()` usage
- Claims speed of about **5ms per MB**

<div class="mt-8" />

> Angular 1 (720KiB) is fully parsed in 5ms, in comparison to the fastest JS parser, Acorn which takes over 100ms.

</v-click>

<!-- 
### Guy Bedford's `es-module-lexer`
- Really great tool for creating module graphs
- Incredibly for static analysis
- Used internally in Node core
- Benchmarks are way above the closest JS alternatives
 -->

---

<Example name="shiki" description="A beautiful Syntax Highlighter" url="https://shiki.matsu.io/" />

<v-click>

```js
import shiki from 'shiki';

const highlighter = await shiki.getHighlighter({ theme: 'github-dark' });
const code = highlighter.codeToHtml(/* source */, { lang: 'js' });
```

</v-click>

<div class="mt-8" />

<v-click>

- High-level JS library, but dependency is written in C
- First JavaScript syntax highlighter with editor-level fidelity (matches [Visual Studio Code](https://code.visualstudio.com/))
- Works with TextMate grammars and Code themes
- Powered by [`vscode-oniguruma`](https://github.com/microsoft/vscode-oniguruma), WebAssembly bindings for [`oniguruma`](https://github.com/kkos/oniguruma) RegExp library

</v-click>

<!-- 
### One of the best examples of WebAssembly's potential, `shiki`
- The kind of package that would have been impossible before Wasm
- Textmate grammars feature incredibly complex Regular Expression syntax
- Semantics are very specific, difficult to emulate in JS
- Every previous highlighter looked "off", Shiki is first with editor-level fidelity
- Output matches Visual Studio Code
- Uses same `oniguruma` bindings as VS Code to execute textmate grammar files
 -->

---

<Example name="goldmark" description="A very fast Markdown compiler for Deno" url="https://deno.land/x/goldmark" />

<v-click>

```ts
import { init, transform } from "https://deno.land/x/goldmark/mod.ts";

await init();
const markdown = await Deno.readTextFile(new URL('./content.md', import.meta.url));
const { frontmatter, content } = await transform(markdown, /* opts */);
```

</v-click>

<div class="mt-8" />

<v-click>

- Written in Go
- WebAssembly bindings for [Goldmark](https://github.com/yuin/goldmark), a CommonMark-compliant Markdown parser
- Original package powers [Hugo](https://gohugo.io/)
- Deno's adherence to web platform spec makes working with WebAssembly easy

<div class="mt-8" />

> Sampling **100,000 runs** completed in **58s** with an average run of **0.57ms** per file.

</v-click>

<!-- 
### One of my own projects, a Deno port of the popular `goldmark` Markdown parser
- Perfect example of Wasm's ability to bridge ecosystem gaps
- Didn't see a Markdown library I liked in Deno, ported one I loved from Go
- Potential for ecosystems to cross-pollinate
- Goldmark powers Hugo, we've discussed a Node port that could be used for Astro
- Deno is all-in on WebAssembly, if you're excited about this space???the innovation is happening in Deno
 -->

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

<!-- 
### Sample of what the incredible `@parcel/css` library can do
- Throw incredibly complex, bleeding-edge CSS at it
- Get small, efficiently down-leveled CSS that works in every browser
 -->

---

<Example name="@parcel/css" description="A CSS parser, transformer, and minifier written in Rust" url="https://github.com/parcel-bundler/parcel-css" />

- Written in Rust
- Lowers modern CSS syntax to be compatible with configurable browser targets
- **Browser-grade** CSS parser, powered by Mozilla's own [`cssparser`](https://github.com/servo/rust-cssparser) and [`selectors`](https://github.com/servo/servo/tree/master/components/selectors) crates

<div class="mt-8" />

<img v-click src="/parcelcss.png" class="w-full" />

<!-- 
### `@parcel/css` part of Parcel bundler
- Main bundler uses Rust-based `swc` package as an alternative to Babel
- Use the exact same crates that power Firefox's CSS! Again, impossible without WebAssembly
 -->

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

**Astro DSL**

```astro {all|1-5|6-19|2,7,13|3,12|4|9|15-19|all}
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

<!-- 
## Spend a bit more time on Astro, since it's the project I'm most involved in.

For some context, Astro has a custom DSL with `.astro` files. 

They're server-side templates that contain some data fetching logic and some markup.
Unlike every other framework which started in the browser and back-ported server compatability,
Astro is proudly designed to run on the server.

Let's take a look at an `.astro` file.

- Frontmatter
- Markup
- Component-based
- Use components from JavaScript Frameworks (React, Svelte, Vue, etc)
  - `client:*` loading directives
- JS with top-level await in frontmatter
- JSX-like expressions
- Automatically scoped styles
-->

---

<Example name="astro" description="A website build tool for the modern web" url="https://github.com/withastro/astro" />

- Compiler is written in Go, rest is JavaScript
- Leverages WebAssembly for compute-heavy tasks, everything else is JavaScript
- Why Go?
  - Iteration speed
  - Proximity to `esbuild`
  - Superset of HTML, borrow from Go's `std` library
- Ability to communicate between JS <=> Wasm

<!-- 
- Compiler written in Go
- Lean on WebAssembly to make compilation performant, everything else can use JavaScript
- Balance was important to keep new contributors interested, compiler in separate repo
- Get a lot of questions why we chose Go (when Rust is so far ahead)
  - Go is fast to learn coming from JavaScript
  - Incredibly fast to prototype
  - Close to `esbuild`, a lot to take inspiration from
  - Spec-compliance is hard, Go had a a `std` module 
- Most exciting feature: the ability to communicate between JS and Wasm
- Would be really complex with old-school native bindings
-->

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

<!-- 
- JS API that we use internally to transform an `.astro` file
- Some Go code which is invoked by `transform`
- Can use a goroutine to block the program while we're waiting for the JS promise to resolve
- Really difficult to directly pass a function reference like this!
-->

---
layout: center
class: "text-center"
---

# WebAssembly doesn't replace JavaScript

<h2 v-click class="opacity-50">Use the best tool (from any ecosystem) for the job</h2>

<!-- 
WebAssembly is not a replacement for JavaScript.
It allows us to use the right tool for the job, regardless of ecosystem
-->

---
layout: center
class: "text-center"
---

# Thank you!

Slides can be found at [nmoo.dev/slides](https://nmoo.dev/slides)

<!-- 
Really appreciate the opportunity to geek out about this stuff!

- Find these slides (and all project links) at `nmoo.dev/slides`
- Find me on Twitter, `@n_moore`
- Check out Astro, `astro.build`
-->
