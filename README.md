# SRLab-YC-Site 專案描述
本專案為詹老師研究室新版網頁的專案，目標是建立一個易於維護與更新的網頁系統。  
## 專案主導  
[@lcabon258](https://github.com/lcabon258)  
# 網站內容  
* 介紹研究室研究主題  
* 研究室主持人介紹  
* 研究室出版文獻  
* 研究團隊介紹  
# 開發工具  
本專案使用 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/) 做為開發工具，[MkDocs](https://www.mkdocs.org/) 為一個以 Python 為基礎的靜態網頁產生器，將 markdown 文件轉換為 html 物件，並依照指定的網站布景（theme）以及插件（plugin）等自動完成排版與搜尋等多樣功能。   
## Markdown
所有文件以 markdown 語法表示，可以參考下面教學與介紹：  
* [Markdown.tw](https://markdown.tw/)
* [Markdown Guide](https://www.markdownguide.org/)
* [Basic writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

# 個人開發環境安裝  
詳細描述請見官方說明：[Getting started](https://squidfunk.github.io/mkdocs-material/getting-started/)  
### Conda  
使用 Conda 安裝：` conda create -n mkdocs -c conda-forge python mkdocs-material`。    
**啟動環境**   
`conda activate mkdocs`   
  
# VSCode IDE 設定
1. 在`Extensions`中搜尋 `YAML` 並安裝延伸功能（或搜尋 [vscode-yaml](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)）。
1. 開啟使用者的 `setting.json`，在`yaml.schemas`中加入以下內容：
  ```json
  {
    "yaml.schemas": {
      "https://squidfunk.github.io/mkdocs-material/schema.json": "mkdocs.yml"
    },
    "yaml.customTags": [ 
      "!ENV scalar",
      "!ENV sequence",
      "tag:yaml.org,2002:python/name:material.extensions.emoji.to_svg",
      "tag:yaml.org,2002:python/name:material.extensions.emoji.twemoji",
      "tag:yaml.org,2002:python/name:pymdownx.superfences.fence_code_format"
    ]
  }

  ```  
# 了解網站架構  
* docs: 網頁內容
  * assets: 網站靜態內容
    * avatar: 頭像圖片
  * news: 部落格 (尚未開通)
    * articles: 部落格文章，目前預計作為摘要、介紹最新研究等項目使用。
    * `index.md`: 部落格主頁。
  * `GM.md`: Group members。
  * `index.md`: 首頁。
  * `PI.md`: 主持人個人介紹。
  * `PubList.md`: 研究室出版清單。
  * `Topics.md`: 介紹研究方向。
* `mkdocs.yml`: 網站設定。
* `README.md`: 本文件。

# 如何更新網站
1. 在本機完成 IDE 環境安裝。
1. 安裝 Github Desktop 或 git 工具。
1. 請 fork 一份專案副本至自己的帳號下。
1. 若需要安裝新功能或更改設定，建議開新的分支（branch），並在 git 中切換至新分支開發。
1. 根據需要更新網站內容。
  * 若為既有檔案：
    1. 直接更新各個網頁（.md）內容。
  * 若建立新檔案：
    1. 單獨頁面：
      1. 在 `docs` 根目錄下建立新的 `.md` 檔。
    1. 群組頁面：
      1. 在 `docs` 建立新資料夾，並有意義的命名。
      1. 在新的資料夾下根據需要建立多個 `.md` 檔，其中 `index.md` 會作為群組的首頁。
      1. 開始編輯內容。
      1. 完成後記得至 `mkdocs.md` 內編輯 `nav:` 清單以顯示頁面在導覽列。
    1. 部落格文章：
      1. 若您還沒有註冊您的名字到作者清單，請更新 `docs/news/.authors.yml` 檔案並輸入您的訊息，否則會報錯：
          ```yml
          authors:
              author1: # 藝名如 github 帳戶或姓名縮寫，此名稱會用在檔頭
                  name: string        # 全名
                  description: string # 描述
                  avatar: url         # 頭像圖片連結網址
              author2:
                  name: string        # Author name
                  description: string # Author description
                  avatar: url         # Author avatar
          ```
      1. 在 `docs/news/articles` 資料夾中建立 `.md` 檔，請以 `{YYYYMMDD}-{slug}.md` 命名。`YYYYMMDD`為日期，`slug`為標題或內容，並以連字號連接長句子。
      1. 新的檔案檔頭需要包含下面的檔頭：
          ```yml
          ---
          date:
            created: 2023-01-31 
            updated: 2023-02-01
          authors:
              - author1 
              - author2 #若有多位作者
          categories:
              - news # 用於研究室新聞或知識介紹等。
              - publication # 用於出版之文章介紹，如摘要等。
          slug: help-im-trapped-in-a-universe-factory
          ---
          # Post title
          ...
          ```
6. 若有新的圖片或靜態檔案請放至 `docs/assets` 內，請注意圖片盡量縮小尺寸以節省線上儲存空間（Github Page 有 1GB 尺寸限制）。
1. 使用 `mkdocs serve` 在本機確認編輯成果。
1. `commit`你的編輯至自己的專案中。
1. 在 Github 網頁上提出 Pull Request:
  1. 按下 `compare across forks`
  1. 主分支選擇如下：`base: repository: SRLab-Code-Club/SRLab-YC-Site` `base: main`（合併至主專案的 main 分支）。
  1. 比較分支選擇如下： `head repository: {你的名稱}/SRLab-YC-Site` `compare: {你的分支/main}`。
1. 管理員會審核你的變更，在同意後會併入本專案的主分支中。  
  
請注意主分支會自動編譯並發布至 Github Page.

# 建立新網站
**本處說明僅作為記錄使用，請注意避免覆蓋本專案內容**，更多細節說明請見 [Create your site](https://squidfunk.github.io/mkdocs-material/creating-your-site/)  
1. 建立新專案：在目前的工作目錄建立新網站：`mkdocs new .`  
### 設定網站參數
開啟 `mkdocs.yml` 設定場景與其他設定，如：
```yml
theme:
    # 設定佈景主題
    name: material
```

## 本機預覽
使用 `mkdocs server` 指令，可啟動及時預覽伺服器，當您儲存專案時會自動重新編譯，在網頁瀏覽器輸入網址`localhost:8000`。

## 本機編譯
使用 `mkdocs build` 將 doc 的內容編譯靜態網頁。
  
## 使用 Github page 自動編譯並部屬網站  
請參閱 [Publishing your site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#github-pages) 一文相關說明。
### Github Action 相關設定   
建立 `.github/workflows/ci.yml` 並填入下面內容：  
```yml
name: ci 
on:
  push:
    branches:
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v3
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material 
      - run: mkdocs gh-deploy --force
```