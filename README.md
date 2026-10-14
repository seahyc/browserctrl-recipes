# browserctrl recipes

Recipes for [browserctrl](https://github.com/seahyc/browserctrl): each one calls a
site's own API from a tab on that site, so an agent gets structured data in
seconds instead of driving the UI for minutes. Requests run inside your logged-in
browser tab, with the site's own cookies and request signing. Recipes contain no
credentials.

## Use

```sh
browserctrl recipe tap add https://github.com/seahyc/browserctrl-recipes
browserctrl recipe find "shopee orders"
browserctrl recipe run shopee.sg/orders --browser dia
```

`browserctrl open`, `nav` and `read` also print a `hint:` line when the page's
site has a recipe here. Update with `browserctrl recipe tap update`.

| Recipe | Returns | Notes |
| --- | --- | --- |
| `shopee.sg/orders` | Full Shopee SG purchase history | |
| `taobao.com/orders` | Full Taobao purchase history (已买到的宝贝) | Needs a tab you opened yourself on 已买到的宝贝; Taobao logs out pages that automation loads |
| `carousell.sg/chats` | Carousell inbox threads, buying and selling | |
| `carousell.sg/messages` | Messages in one Carousell chat | Pass `offer_id=` (the `offer_id` field) from `carousell.sg/chats`; needs browserctrl with WebSocket capture |
| `carousell.sg/orders` | Carousell checkout purchases for one tab | Item shape not yet observed |

## Contribute

A recipe is `<site>/<name>.json`; the format is in
[browserctrl's references/recipes.md](https://github.com/seahyc/browserctrl/blob/main/references/recipes.md).
browserctrl records the fetch/XHR traffic of tabs it drives, so
`browserctrl recipe endpoints <host>` and `recipe inspect <host> <match>` show
what a page called. Before opening a pull request:

- Run it with `browserctrl recipe run` and check it returns the same facts the UI
  shows. Describe that in `verified`, without personal data.
- Keep it free of tokens, cookies, account ids and other personal values: auth is
  a source (`cookie`, `html`) read when the recipe runs.
- Mark anything that changes data as `"kind": "write"`.

Recipes use sites' internal APIs, which can change without notice. You are
responsible for using them within each site's terms.

MIT licensed.
