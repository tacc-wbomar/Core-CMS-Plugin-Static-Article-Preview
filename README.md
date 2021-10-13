## Texas Advanced Computing Center
# Django CMS Plugin: "(Static) Article Preview"

This plugin renders a static preview of content from an article.

- __`__plugin_name__`__: `taccsite_static_article_preview`
- __`__PluginName__`__: `TaccsiteStaticArticlePreview`
- __"Plugin Name"__: "(Static) Article Preview"

<details><summary>Intent</summary>

_This plugin only exists because of the unavailaibility of a solution to sync news between two TACC websites. To learn more, see [TACC/Core-CMS wiki page "Static-Article-Plugins"][tacc-sa-plugins]._

</details>

## Quick Start

1. Follow https://github.com/tacc-wbomar/Core-CMS-Plugin/wiki/Core-CMS-Plugin-Usage-Quick-Start.

## Usage

1. Add instance of [`taccsite_static_article_list`][tacc-sa-list] to a page.
1. Configure the plugin instance.
1. Add instance of this plugin within a [`taccsite_static_article_list`][tacc-sa-list].
1. See plugin render content that matches configuration.

## Features

1. Render an `<article>` with content using semantic markup.
2. Support previews of different kinds of articles.
    <details>

    | kind | description | content |
    | :- | :- | :- |
    | News | [external news articles][tacc-sa-plugins] | image, type, date published, title, abstract |
    | Documents | [single-topic documents][tacc-core-docs] | title, abstract |
    | Allocations | [date range for applications][fp-allocs] | image, title, date (or range) |
    | Events | [learning opportunities][tacc-learn] | date (or range), title, abstract |

    </details>

3. Only supported as nested within [`taccsite_static_article_list`][tacc-sa-list] of the same kind.
4. Inteligently renders date or date range for some kinds of articles.

    <details>

    | kind | outputs |
    | :- | :- |
    | Allocations | date or range (with appropriate English) |
    | Events | date or range (with dash "–" as needed) |

    | render method | for which dates |
    | :- | :- |
    | range | a date range within which the current date lies |
    | next future date | a publish and/or expiry date that is in the future |
    | last past date | a publish and/or expiry date that is in the past |

    For examples of Allocation dates, see [`docs/allocation-dates.md`](https://github.com/tacc-wbomar/Core-CMS-Plugin-Static-Article-Preview/blob/main/docs/allocation-dates.md).

    </details>
5. Renders supported, nested plugin instances to incorporate extra content.
    <details>

    | content | supported by |
    | :- | :- |
    | image | [`djangocms-picture`][dcms-picture] |
    |   "   | [`djangocms_bootstrap4`][dcms-bs4]'s [`bootstrap4_picture`][bs4-picture] |

    </details>
6. Uses supported, integrated plugin instances to incorporate extra features.
    <details>

    | feature | supported by |
    | :- | :- |
    | article preview as hyperlink | [`taccsite_data_list`][dcms-link] |

    </details>
7. Supports (but does not render) author.

## Caveats

- Requires [`djangocms_link`][dcms-link].\*
- Expects [`taccsite_static_article_list`][tacc-sa-list].†
- Hyperlink is within title tag (does not wrap article).‡

> \* Support is mandatory, but should become optional in a future release.
>
> † A plugin instance is not allowed except inside this parent plugin.
>
> ‡ So the entire article is not a link. To add this support to your app, [stretch the link](https://github.com/TACC/Core-CMS/blob/b028b59/taccsite_cms/static/site_cms/css/src/_imports/tools/x-article-link.css#L20-L29). To add this support to this app, this plugin could [render `<a>` like `taccsite_callout`](https://github.com/tacc-wbomar/Core-CMS-Plugin-Callout/blob/7d287a9/taccsite_callout/templates/callout.html#L12-L25).



[fp-allocs]: https://frontera-portal.tacc.utexas.edu/allocations/

[tacc-learn]: https://learn.tacc.utexas.edu/
[tacc-core-docs]: https://cep.tacc.utexas.edu/guides/
[tacc-sa-plugins]: https://github.com/TACC/Core-CMS/wiki/Static-Article-Plugins
[tacc-sa-list]: https://github.com/tacc-wbomar/Core-CMS-Plugin-Static-Article-List

[dcms-link]: https://github.com/django-cms/djangocms-link
[dcms-picture]: https://github.com/django-cms/djangocms-picture

[dcms-bs4]: https://github.com/django-cms/djangocms-bootstrap4
[bs4-picture]: https://github.com/django-cms/djangocms-bootstrap4/tree/master/djangocms_bootstrap4/contrib/bootstrap4_picture
