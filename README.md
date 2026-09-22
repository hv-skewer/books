# 上书单 · 藏书转让

一个纯静态的售书页：56 本书，逐本实拍封面，按类别可筛、可搜、可打印清单。
卖掉一本，点一下就会打上大字「已售出」。

---

## 一、怎么发到网上（5 分钟）

### 第 1 步：建仓库
1. 打开 <https://github.com/new>
2. **Repository name** 填一个名字，例如 `books`
3. 选 **Public**（Pages 免费版需要公开仓库）
4. 点 **Create repository**

### 第 2 步：把本文件夹里的东西全部传上去
在本文件夹里**全选所有文件和文件夹**（`index.html`、`data`、`images`、`thumbs`、`README.md`、`.nojekyll`），
在仓库页面点 **Add file → Upload files**，把它们拖进去，然后 **Commit changes**。

> ⚠️ `.nojekyll` 是隐藏文件（文件名以点开头）。如果拖拽时看不到它，没关系——少了它页面一样能开，只是多走一道 Jekyll 处理。想补的话：Add file → Create new file，文件名写 `.nojekyll`，内容留空，提交即可。
>
> ⚠️ 上传时**要保持目录结构**：`images/` 和 `thumbs/` 必须是文件夹，不能被拍平成一层。

### 第 3 步：打开网站
1. 仓库页 → **Settings** → 左侧 **Pages**
2. **Source** 选 `Deploy from a branch`，**Branch** 选 `main`，目录选 `/ (root)`，点 **Save**
3. 等 1 分钟左右，刷新该页，会出现网址：

```
https://<你的用户名>.github.io/books/
```

这个链接可以直接发给别人。

---

## 二、怎么标记「卖掉了」

打开网站 → 点任意一本书 → 右下角 **「标记为已售出」**。

- 卡片会立刻变成黑白，并盖上大字 **已售出**，清单视图里也会显示「已售出」。
- 这个状态默认**存在你自己的浏览器里**，刷新不丢，但**别人打开链接看不到**。

想让所有人都看到，有两种办法：

### 办法 A：点「上传到仓库」（推荐）
1. 网页右上角点 **管理**
2. 填三项：
   - **GitHub**：`用户名/仓库名`，例如 `caspiran/books`
   - **分支**：`main`
   - **Token**：去 <https://github.com/settings/personal-access-tokens/new> 建一个**细粒度 token**
     - Repository access → Only select repositories → 选这个仓库
     - Permissions → Repository permissions → **Contents: Read and write**
     - 生成后复制那串 `github_pat_...` 填进来
3. 点 **上传到仓库**。它会更新 `data/state.json`，GitHub Pages 大约 1 分钟后重新发布，别人刷新就能看到。

> Token 只存在你这台电脑的浏览器里，不会写进代码、也不会泄露到页面上。随时可以在 GitHub 撤销。
> 换电脑要重新填一次。

### 办法 B：导出文件手动提交
点 **导出 JSON 备份** → 得到 `state.json` → 在 GitHub 网页上把 `data/state.json` 覆盖提交。

---

## 三、改价格 / 改联系方式

- **价格**：点开一本书，在「定价 ¥」里填数字，回车。会跟着 `state.json` 一起上传。
- **联系方式**：管理面板里的「联系人 / 联系方式」，填完会显示在页面顶部。

---

## 四、目录结构

```
index.html          页面本体（图书数据已内嵌，双击即可离线打开）
data/books.json     图书数据（书名/作者/出版社/类别）
data/books.csv      同上的表格版，Excel 可直接打开（带 BOM，不乱码）
data/state.json     售出状态与定价（由网页上传更新）
images/             网页大图 1400px，共 56 张
thumbs/             列表缩略图 520px，共 56 张
.nojekyll           告诉 GitHub Pages 不要用 Jekyll 处理
```

## 五、本地预览

直接双击 `index.html` 就能看（图片用的是相对路径，离线正常）。
唯一在离线时不工作的是「上传到仓库」和自动同步——那两个需要真正跑在 http(s) 上。

---

### 数据是怎么来的

原始照片在 `E:\DOCHUMAN\Project-UNAMED\Workbuddy\书籍图片`（未改动），
全部顺时针旋转 90° 后的全分辨率版本在 `书籍图片_摆正\`。
封面上的书名/作者/出版社是逐本看图录入的，`DSCN` 编号与原始文件名一一对应，可回溯核对。
