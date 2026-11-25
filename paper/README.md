# ICEIB 2027 — GarbageGo (IEEE Conference Paper)

**GarbageGo: A Domain AI Agent for Time-Feasibility Recommendation of Garbage Collection Points Using Low-Frequency Open Data**

ICEIB 2027（7th International Conference on Electronic Communications, Internet of Things and Big Data）投稿用 LaTeX 專案，採 IEEEtran conference 版型。內容改寫自 GarbageGo repo 的 `docs/proposal/proposal-integrated.md`、`DESIGN.md` 與 `docs/research/` 實測報告。

- 全文篇幅：4–8 頁
- 摘要截止：2027/03/01
- 全文截止：2027/04/20（Important Dates 頁另列 final paper 2027/06/30，需向主辦單位確認）
- 注意：官網目前列的是 MDPI *Engineering Proceedings* (.docx) 模板，IEEE 格式是否適用請先與主辦單位確認

## 目錄結構

```
ICEIB2027-IEEE/
├── main.tex                 # 主檔：標題、作者、\input 各章節、參考文獻
├── references.bib           # BibTeX 參考文獻
├── README.md
├── sections/
│   ├── 00_abstract.tex      # 摘要 + IEEE Keywords
│   ├── 01_introduction.tex
│   ├── 02_related_work.tex
│   ├── 03_proposed_scheme.tex   # 架構、slack 公式、Algorithm 1、LLM 角色
│   ├── 04_experiments.tex   # 資料可行性實測 + 評估計畫（無推薦實驗結果）
│   └── 05_conclusion.tex
├── figures/
│   └── architecture.pdf     # 系統架構圖 ①–⑨（TikZ 繪製），可用同檔名覆蓋
└── tables/
    └── comparison.tex       # 與既有服務能力比較（Table I，由 02_related_work 引用）
```

## 編譯

**Overleaf**：上傳整個 zip（New Project → Upload Project），主檔設為 `main.tex`。IEEEtran 已內建。

**本機**（需 TeX Live，IEEEtran 在 `texlive-publishers` 套件內）：

```bash
latexmk -pdf main.tex
# 或
pdflatex main && bibtex main && pdflatex main && pdflatex main
```

清除暫存檔：`latexmk -c`

## 撰寫慣例

| 項目 | 規則 |
|---|---|
| 章節標籤 | `sec:intro` / `sec:related` / `sec:scheme` / `sec:exp` / `sec:conclusion` |
| 圖 | 放 `figures/`，以 `\figureorplaceholder{檔名}{\columnwidth}` 或 `\includegraphics` 引用；caption 在圖**下方**；引用寫 `Fig.~\ref{fig:xxx}` |
| 表 | 一張表一個檔放 `tables/`，在章節中 `\input{tables/xxx}`；caption 在表**上方**；引用寫 `Table~\ref{tab:xxx}` |
| 公式 | `\eqref{eq:xxx}`；符號在公式後立即定義 |
| 文獻 | `\cite{key}`，只有被引用的條目會出現在 References |
| 跨欄圖表 | 使用 `figure*` / `table*`，寬度 `\textwidth` |

## 新增圖片

1. 將圖檔（建議向量 PDF）放進 `figures/`
2. 在章節中：

```latex
\begin{figure}[htbp]
\centerline{\includegraphics[width=\columnwidth]{architecture.pdf}}
\caption{System architecture of the proposed scheme.}
\label{fig:arch}
\end{figure}
```

## 投稿前待辦（內容）

- [ ] 作者羅馬拼音、系所、Email（`main.tex`，目前只填了 An-Jyue Lee）
- [ ] 指導教授列為作者或寫在 Acknowledgment
- [ ] 確認 `safety_buffer` 的線性形式（式 2）組內是否同意——這是論文新增的形式化，`DESIGN.md` 尚未定義
- [ ] 推薦實驗完成後，補上 Results 小節（目前只有資料可行性與評估計畫）
- [ ] 確認 ICEIB 是否接受 IEEE 格式（官網列的是 MDPI Engineering Proceedings 模板）

## 投稿前檢查

- [ ] 頁數 4–8 頁
- [ ] 所有 `Missing figure` 佔位框都已替換
- [ ] 作者資訊、Acknowledgment 已填寫（雙盲審查則先移除）
- [ ] 編譯無 `??`（未解析的 `\ref` / `\cite`）
- [ ] 字型全部嵌入：`pdffonts main.pdf`，emb 欄皆為 `yes`
