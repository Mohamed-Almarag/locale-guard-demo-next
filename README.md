# Locale Guard demo: Next.js with next-intl

A small Next.js shop in English, Arabic, French and German, translated with
[next-intl](https://next-intl.dev). Messages use ICU syntax: plurals, selects
and rich text tags. It shows what
[Locale Guard](https://github.com/Mohamed-Almarag/locale-guard) reports on real
pull requests.

## Setup

| | |
|---|---|
| Framework | Next.js 16, App Router |
| Translation library | `next-intl` (ICU messages) |
| Locale files | `messages/{locale}.json`, one file per language |
| Base locale | `en` |

The whole setup is one workflow file,
[.github/workflows/translations.yml](.github/workflows/translations.yml):

```yaml
- uses: Mohamed-Almarag/locale-guard@v1
  with:
    files: messages/{locale}.json
    format: next-intl
```

## Pull requests to look at

| Pull request | What it shows | Result |
|---|---|---|
| [#1 Add the cart](https://github.com/Mohamed-Almarag/locale-guard-demo-next/pull/1) | A plural without the `other` form, Arabic plural forms that are missing, a renamed `select` argument, a missing rich text tag, a message that does not compile, a missing key, untranslated text and an extra key | ❌ Fails |
| [#2 Add order tracking](https://github.com/Mohamed-Almarag/locale-guard-demo-next/pull/2) | The first commit forgets French and German, the second one adds them, and the same comment turns green | ✅ Passes |
| [#3 Lay out products in a grid](https://github.com/Mohamed-Almarag/locale-guard-demo-next/pull/3) | A change that touches no translation file, so the check finishes in seconds | ✅ Passes |

The `main` branch already has two old issues: a key German never got, and an
Arabic plural with three of its six forms. Locale Guard lists them apart from the
issues each pull request adds, collapsed, and they do not fail the check.

## Run the shop

```bash
npm install
npm run dev
```
