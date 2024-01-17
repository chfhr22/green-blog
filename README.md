# A statically generated blog example using Next.js, Markdown, and TypeScript

This is the existing [blog-starter](https://github.com/vercel/next.js/tree/canary/examples/blog-starter) plus TypeScript.

This example showcases Next.js's [Static Generation](https://nextjs.org/docs/basic-features/pages) feature using Markdown files as the data source.

The blog posts are stored in `/_posts` as Markdown files with front matter support. Adding a new Markdown file in there will create a new blog post.

To create the blog posts we use [`remark`](https://github.com/remarkjs/remark) and [`remark-html`](https://github.com/remarkjs/remark-html) to convert the Markdown files into an HTML string, and then send it down as a prop to the page. The metadata of every post is handled by [`gray-matter`](https://github.com/jonschlinkert/gray-matter) and also sent in props to the page.

## Demo

[https://next-blog-starter.vercel.app/](https://next-blog-starter.vercel.app/)

## Deploy your own

Deploy the example using [Vercel](https://vercel.com?utm_source=github&utm_medium=readme&utm_campaign=next-example) or preview live with [StackBlitz](https://stackblitz.com/github/vercel/next.js/tree/canary/examples/blog-starter)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/vercel/next.js/tree/canary/examples/blog-starter&project-name=blog-starter&repository-name=blog-starter)

### Related examples

- [WordPress](/examples/cms-wordpress)
- [DatoCMS](/examples/cms-datocms)
- [Sanity](/examples/cms-sanity)
- [TakeShape](/examples/cms-takeshape)
- [Prismic](/examples/cms-prismic)
- [Contentful](/examples/cms-contentful)
- [Strapi](/examples/cms-strapi)
- [Agility CMS](/examples/cms-agilitycms)
- [Cosmic](/examples/cms-cosmic)
- [ButterCMS](/examples/cms-buttercms)
- [Storyblok](/examples/cms-storyblok)
- [GraphCMS](/examples/cms-graphcms)
- [Kontent](/examples/cms-kontent)
- [Umbraco Heartcore](/examples/cms-umbraco-heartcore)
- [Builder.io](/examples/cms-builder-io)
- [TinaCMS](/examples/cms-tina/)
- [Enterspeed](/examples/cms-enterspeed)

## How to use

Execute [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) with [npm](https://docs.npmjs.com/cli/init), [Yarn](https://yarnpkg.com/lang/en/docs/cli/create/), or [pnpm](https://pnpm.io) to bootstrap the example:

```bash
npx create-next-app --example blog-starter blog-starter-app
```

```bash
yarn create next-app --example blog-starter blog-starter-app
```

```bash
pnpm create next-app --example blog-starter blog-starter-app
```

Your blog should be up and running on [http://localhost:3000](http://localhost:3000)! If it doesn't work, post on [GitHub discussions](https://github.com/vercel/next.js/discussions).

Deploy it to the cloud with [Vercel](https://vercel.com/new?utm_source=github&utm_medium=readme&utm_campaign=next-example) ([Documentation](https://nextjs.org/docs/deployment)).

# Notes

`blog-starter` uses [Tailwind CSS](https://tailwindcss.com) [(v3.0)](https://tailwindcss.com/blog/tailwindcss-v3).

## 시작하기

[vercel](https://vercel.com/templates/next.js/blog-starter-kit)

npx create-next-app --example blog-starter blog-starter-app

## next.config.js 추가 및 수정

```js
/\*\*

- @type {import('next').NextConfig}
  \*/
  const nextConfig = {
  output: 'export',

// Optional: Change links `/me` -> `/me/` and emit `/me.html` -> `/me/index.html`
// trailingSlash: true,

// Optional: Prevent automatic `/me` -> `/me/`, instead preserve `href`
// skipTrailingSlashRedirect: true,

// Optional: Change the output directory `out` -> `dist`
// distDir: 'dist',
}

module.exports = nextConfig
```

distDir: 'dist'의 주석을 풀고

```js
images: {
  unoptimized: true;
}
```

이 소스를 추가

## build 및 깃 등록

npm run build 후 git에 등록한 뒤에

settings > pages > Build and deployment의 Source를 GitHub Actions로 변경

## 설정 변경

.github > workflows > nextjs.yml에서

```js
- name: Install dependencies
        run: ${{ steps.detect-package-manager.outputs.manager }} ${{ steps.detect-package-manager.outputs.command }}
      - name: Build with Next.js
        run: ${{ steps.detect-package-manager.outputs.runner }} next build
      - name: Static HTML export with Next.js
        run: ${{ steps.detect-package-manager.outputs.runner }} next export
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./out
```

위의 소스를 찾은 후

```js
- name: Static HTML export with Next.js
        run: ${{ steps.detect-package-manager.outputs.runner }} next export
```

해당 소스를 지우고
path를 out에서 dist로 변경

## 이미지 경로 수정
