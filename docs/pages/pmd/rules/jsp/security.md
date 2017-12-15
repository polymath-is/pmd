---
title: Security
summary: Rules that flag potential security flaws.
permalink: pmd_rules_jsp_security.html
folder: pmd/rules/jsp
sidebaractiveurl: /pmd_rules_jsp.html
editmepath: ../pmd-jsp/src/main/resources/category/jsp/security.xml
keywords: Security, IframeMissingSrcAttribute, NoUnsanitizedJSPExpression
---
## IframeMissingSrcAttribute

**Since:** PMD 3.6

**Priority:** Medium High (2)

IFrames which are missing a src element can cause security information popups in IE if you are accessing the page
through SSL. See http://support.microsoft.com/default.aspx?scid=kb;EN-US;Q261188

```
//Element[upper-case(@Name)="IFRAME"][count(Attribute[upper-case(@Name)="SRC" ]) = 0]
```

**Example(s):**

``` jsp
<HTML><title>bad example><BODY>
<iframe></iframe>
</BODY> </HTML>

<HTML><title>good example><BODY>
<iframe src="foo"></iframe>
</BODY> </HTML>
```

**Use this rule by referencing it:**
``` xml
<rule ref="category/jsp/security.xml/IframeMissingSrcAttribute" />
```

## NoUnsanitizedJSPExpression

**Since:** PMD 5.1.4

**Priority:** Medium (3)

Avoid using expressions without escaping / sanitizing. This could lead to cross site scripting - as the expression
would be interpreted by the browser directly (e.g. "<script>alert('hello');</script>").

**This rule is defined by the following Java class:** [net.sourceforge.pmd.lang.jsp.rule.security.NoUnsanitizedJSPExpressionRule](https://github.com/pmd/pmd/blob/master/pmd-jsp/src/main/java/net/sourceforge/pmd/lang/jsp/rule/security/NoUnsanitizedJSPExpressionRule.java)

**Example(s):**

``` jsp
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
${expression}                    <!-- don't use this -->
${fn:escapeXml(expression)}      <!-- instead, escape it -->
<c:out value="${expression}" />  <!-- or use c:out -->
```

**Use this rule by referencing it:**
``` xml
<rule ref="category/jsp/security.xml/NoUnsanitizedJSPExpression" />
```
