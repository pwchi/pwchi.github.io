<!--
.. title: 不同 Hexo render 顯示 markdown table 的比較
.. slug: 不同 Hexo render 顯示 markdown table 的比較
.. date: 2016-04-29 02:47:23 UTC+08:00
.. tags: Hexo, markdown
.. category:
.. link:
.. description:
.. type: text
-->
為了瞭解 **hexo-renderer-markdown-it** 與 **hexo-renderer-pandoc** 在顯示表格上的差異，我將下列 markdown table 餵為給兩套 render ，分別觀察他們的結果。

## 原始 markdown 表格 code 如下

```
| Right | Left | Default | Center |
|------:|:-----|---------|:------:|
|   12  |  12  |    12   |    12  |
|  123  |  123 |   123   |   123  |
|    1  |    1 |     1   |     1  |
```

## hexo-renderer-markdown-it render 出來的表格

![hexo-renderer-markdown-it render 出來的表格](/2016-04-29-不同-Hexo-render-顯示-markdown-table-的比較/hexo_it_table.png "hexo-renderer-markdown-it render 出來的表格")

## hexo-renderer-pandoc redner 搭配 pandoc 1.17.0.2 render 出來的表格

![hexo-renderer-pandoc redner 搭配 pandoc 1.17.0.2 render 出來的表格](/2016-04-29-不同-Hexo-render-顯示-markdown-table-的比較/hexo_pandoc_table.png "hexo-renderer-pandoc redner 搭配 pandoc 1.17.0.2 render 出來的表格")

結論

 - **hexo-renderer-markdown-it** 較能正確顯示 markdown table 的對齊樣式。
 - **hexo-renderer-pandoc** 雖無法正確對齊，但支援較多種表格形式。
