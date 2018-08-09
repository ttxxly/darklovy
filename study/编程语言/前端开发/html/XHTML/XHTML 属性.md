**XHTML 属性是以 XML 格式编写的 HTML 属性。**

## XHTML 属性 - 语法规则

- XHTML 属性必须使用*小写*
- XHTML 属性值必须用*引号包围*
- XHTML 属性最小化也是*禁止的*

## XHTML 属性必须使用小写

这是错误的：

```
<table WIDTH="100%">
```

这是正确的：

```
<table width="100%">
```

## XHTML 属性值必须用引号包围

这是错误的：

```
<table width=100%>
```

这是正确的：

```
<table width="100%">
```

## 禁止属性简写

这是错误的：

```
<input checked>
<input readonly>
<input disabled>
<option selected>

```

这是正确的：

```
<input checked="checked" />
<input readonly="readonly" />
<input disabled="disabled" />
<option selected="selected" />
```