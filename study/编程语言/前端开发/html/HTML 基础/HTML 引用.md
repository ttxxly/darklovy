这是摘自 WWF 网站的引文：

> 五十年来，WWF 一直致力于保护自然界的未来。 世界领先的环保组织，WWF 工作于 100 个国家，并得到美国一百二十万会员及全球近五百万会员的支持。

#### HTML <q> 用于短的引用

浏览器通常为 <q> 元素包围引号。

```
<p>WWF 的目标是：<q>构建人与自然和谐共存的世界。</q></p>
```

#### 用于长引用的 HTML <blockquote>

浏览器通常会对 <blockquote> 元素进行缩进处理

```
<p>以下内容引用自 WWF 的网站：</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>
```

#### 用于缩略词的 HTML <abbr>

HTML <abbr> 元素定义缩写或首字母缩略语

对缩写进行标记能够为浏览器、翻译系统以及搜索引擎提供有用的信息。

```
<p><abbr title="World Health Organization">WHO</abbr> 成立于 1948 年。</p>
```

#### 用于定义的HTML <dfn>

HTML <dfn> 元素定义项目或缩写的定义。

<dfn> 的用法相对比较复杂。

1. 如果设置了 <dfn> 元素的 title 属性：

   ```
   <p><dfn title="World Health Organization">WHO</dfn> 成立于 1948 年。</p>
   ```

2. 如果 <dfn> 元素包含具有标题的 <abbr> 元素，则 title 定义项目：

   ### 实例

   ```
   <p><dfn><abbr title="World Health Organization">WHO</abbr></dfn> 成立于 1948 年。</p>

   ```

   [亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_dfn_2)

3. 否则，<dfn> 文本内容即是项目，并且父元素包含定义。

   ### 实例

   ```
   <p><dfn>WHO</dfn> World Health Organization 成立于 1948 年。</p>

   ```

   [亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_dfn_3)

   注释：如果您希望简而化之，请使用第一条，或使用 <abbr> 代替。

## 用于联系信息的 HTML <address>

HTML *<address>* 元素定义文档或文章的联系信息（作者/拥有者）。

此元素通常以*斜体*显示。大多数浏览器会在此元素前后添加折行。

### 实例

```
<address>
Written by Donald Duck.<br> 
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_address)

## 用于著作标题的 HTML <cite>

HTML *<cite>* 元素定义*著作的标题*。

浏览器通常会以斜体显示 <cite> 元素。

### 实例

```
<p><cite>The Scream</cite> by Edward Munch. Painted in 1893.</p>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_cite)

## 用于双向重写的 HTML <bdo>

HTML *<bdo>* 元素定义双流向覆盖（bi-directional override）。

<bdo> 元素用于覆盖当前文本方向：

### 实例

```
<bdo dir="rtl">This text will be written from right to left</bdo>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_bdo)