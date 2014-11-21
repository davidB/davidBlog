---
title: "use compact syntax"
description": ""
date: "2006-06-15"
categories: ["articles"]
tags: [ "lang/xsl", "convention"]
---

Some tips about xsl writing:

* remove useless template, parameter,...
* for attribute definition, use compact syntax instead of <xsl:attribute> and <xsl:value-of>

replace:

```
  <toto>
    <xsl:attribute name=&quot;foo&quot;><xsl:value-of select=&quot;/x/z&quot;/></xsl:attribute>
    ...
  </toto>
```

by:

```
  <toto foo=&quot;\{/x/z\}&quot;>
    ...
  </toto>
```

*   don't use <xsl:attribute> if the attribute is always present and the value is constante.

replace:

```
  <toto>
    <xsl:attribute name=&quot;foo&quot;>bar</xsl:attribute>
    ...
  </toto>
```

by:

```
  <toto foo=&quot;bar&quot;>
    ...
  </toto>
```

*   use compact empty node syntax

replace:

```
  <toto>
  </toto>
```

by:

```
  <toto/>
```

*   use <xsl:if> instead of <xsl:choose> with 2 choices, if possible

replace:

```
  <table>
    <xsl:choose>
      <xsl:when test=&quot;/page/data/notfirsttime ='no'&quot;>
        <tr>
        </tr>
      </xsl:when>
      <xsl:otherwise>
        <tr>
          <td>Rows Fetched:</td>
          <td><xsl:value-of select=&quot;data/totalrows&quot;/></td>
        </tr>
      </xsl:otherwise>
    </xsl:choose>
  </table>
```

by:

```
  <table>
    <tr>
      <xsl:if test=&quot;/page/data/notfirsttime !='no'&quot;>
        <td>Rows Fetched:</td>
        <td><xsl:value-of select=&quot;data/totalrows&quot;/></td>
      </xsl:if>
    </tr>
  </table>
```
