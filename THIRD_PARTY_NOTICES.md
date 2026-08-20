# Third-Party Notices

**第三方组件与材料声明**

*Last updated: 2026-08-20*

This file lists third-party software, themes and materials used by or reproduced in this knowledge base. **None of the items below are the copyright of 张素俊Allen**, and the repository's own [Copyright and Usage Notice](LICENSE.md) does not apply to them.

本文件列出本知识库使用或转载的第三方软件、主题与材料。**以下各项均非张素俊Allen 的版权财产**，本仓库的版权声明不适用于它们。

---

## Software components 软件组件

| Component | Source | Licence | Copyright |
|---|---|---|---|
| **Minima** (Jekyll theme) | [jekyll/minima](https://github.com/jekyll/minima) | MIT | © Jekyll contributors |
| **jekyll-sitemap** | [jekyll/jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap) | MIT | © Jekyll contributors |
| **jekyll-seo-tag** | [jekyll/jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) | MIT | © Jekyll contributors |
| **Jekyll** | [jekyll/jekyll](https://github.com/jekyll/jekyll) | MIT | © Tom Preston-Werner and Jekyll contributors |
| **GitHub Pages build pipeline** | GitHub Actions (`actions/jekyll-build-pages`, `actions/deploy-pages`) | MIT | © GitHub, Inc. |

These components retain their original licences in full. Their licence terms are not superseded, modified, or re-licensed by anything in this repository.

以上组件完整保留其原始许可证。本仓库的任何内容均不取代、修改或重新许可这些条款。

### Theme override 主题覆盖文件

`_layouts/default.html` in this repository is a **minimal local override** of Minima's layout of the same name. It reproduces Minima's structure and adds a single footer line carrying the copyright notice and a link to the reuse policy.

本仓库的 `_layouts/default.html` 是对 Minima 同名布局的**最小化本地覆盖**：复制其结构，并追加一行页脚，用于显示版权声明与复用政策链接。

> **Maintenance note 维护提示**：because this file duplicates upstream structure, a future Minima upgrade may change the original without changing this override. If the site layout ever looks wrong after a theme update, compare this file against the current Minima `default.html` first.
>
> 由于该文件复制了上游结构，未来 Minima 升级可能改动原文件而不影响本覆盖文件。主题更新后若页面布局异常，请先比对本文件与当时的 Minima `default.html`。

---

## Reproduced third-party content 转载的第三方内容

### KDD 2024 GEO paper — Chinese translation

| | |
|---|---|
| **Page 页面** | `geo-paper-kdd2024-zh.md` |
| **Original work** | *GEO: Generative Engine Optimization*, Aggarwal et al. |
| **Published** | KDD 2024 · DOI [10.1145/3637528.3671900](https://doi.org/10.1145/3637528.3671900) · [arXiv:2311.09735](https://arxiv.org/abs/2311.09735) |
| **Original licence** | **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)** |
| **Status here** | Chinese translation — a **marked adaptation**, provided under **CC BY 4.0** |
| **Rights in the original** | Held entirely by the original authors |

The translation is **not** covered by the repository's "all rights reserved" terms. Nothing in this repository restricts any right that CC BY 4.0 grants in the underlying paper. The translation does not imply endorsement by the original authors or their institutions.

该译本**不**适用本仓库的"保留全部权利"条款。本仓库任何内容均不限制 CC BY 4.0 就原论文授予的权利。译本不代表原作者或其所属机构的背书。

### Evidence screenshot 证据截图

| | |
|---|---|
| **File** | `assets/evidence-001-wechat-ai-search.jpg` |
| **Content** | A screenshot of a third-party AI search product's result page, retained as dated evidence for the GEO lab record |
| **Rights** | Interface elements and any third-party text shown remain the property of their respective owners |
| **Basis of use** | Quotation for the purpose of comment, review and record |

No ownership is claimed over the third-party interface or content depicted.

对截图中的第三方界面与内容不主张任何所有权。

---

## Quoted primary sources 所引一手材料

This knowledge base quotes, cites and analyses official and third-party texts. **All rights remain with their respective owners**, and quotation here is for the purposes of research, commentary and education, with sources identified so that readers can verify against the originals.

本知识库引用、援引并分析官方与第三方文本。**全部权利归其各自权利人**；此处引用用于研究、评论与教育，并标明出处以便读者回到原文核对。

Principal categories:

- **OECD** — Common Reporting Standard and related publications
- **People's Republic of China** — State Council decrees and normative documents (including Decree No. 837, Guo Ban Fa [2024] No. 38), tax laws and announcements
- **Hong Kong SAR** — Inland Revenue Ordinance, bills and gazette notices
- **Regulators** — Hong Kong Insurance Authority; National Financial Regulatory Administration; National Healthcare Security Administration; State Taxation Administration and provincial tax bureaux; Shanghai Municipal Healthcare Security Administration
- **Industry bodies** — Insurance Association of China (中国保险行业协会); Hong Kong Federation of Insurers (HKFI)
- **Insurers** — policy wordings and public solvency disclosures
- **Academic and media** — cited papers and news reports, attributed individually within each entry

Where a quotation is reproduced, the entry states the document name and, where available, the clause number, so the reader can check the original rather than rely on this knowledge base's rendering of it.

凡逐字引用之处，条目均标明文件名称及（如有）条款编号，以便读者核对原文，而非依赖本知识库的转述。

---

## Build-time dependencies 构建期依赖

Beyond the plugins declared in `_config.yml` (`jekyll-sitemap`, `jekyll-seo-tag`), this site
relies on plugins bundled by **GitHub Pages** (the `github-pages` gem, via
`actions/jekyll-build-pages`). They are declared nowhere in this repository, but the site does
not render correctly without them.

| Plugin | What it does here | Licence |
|---|---|---|
| `jekyll-optional-front-matter` | Renders `.md` files carrying no front matter (README, about, geo-lab, this file) | MIT |
| `jekyll-relative-links` | Rewrites in-body `xxx.md` links to their built `.html` URLs | MIT |
| `jekyll-readme-index` | Serves `README.md` as the site index (there is no `index.md`) | MIT |
| `jekyll-titles-from-headings` | Derives a page title from the first `# heading` where none is set | MIT |
| `jekyll-default-layout` | Applies the theme layout to pages that declare none | MIT |

以上插件由 GitHub Pages 构建环境提供，均为 MIT 授权，版权归各自作者所有。
**迁移提示**：若改用自建 Jekyll 构建，须先为上述页面补 front matter、并将正文内链改为
`.html`，否则整站页面将退化为静态文件而无法访问。

---

*Corrections to this file are welcome. If you hold rights in material listed here and believe the attribution is wrong or incomplete, please raise an issue or use the contact channel on the [About](about.md) page.*

*欢迎对本文件提出更正。若您对此处所列材料享有权利，且认为署名有误或不完整，请提交 Issue 或通过[关于作者](about.md)页面所列渠道联系。*
