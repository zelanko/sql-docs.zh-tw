---
title: XSLT 轉換 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1e443a2c131fc2338660c6ddfd0a09b285e1dba0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699725"
---
# <a name="xslt-transformations"></a>XSLT 轉換
XSLT 可以套用至所產生的 XML，將它轉換成另一種格式。 了解在 ADO 中的 XML 格式，可以協助開發 XSLT 範本可以將它轉換成更方便使用的表單。  
  
 例如，您會知道資料錄集的每個資料列會儲存為 rs： 資料元素內的 z： 資料列項目。 同樣地，每個資料錄集的欄位會儲存為此元素的屬性 / 值組。  
  
## <a name="remarks"></a>備註  
 下列 XSLT 指令碼可以套用至的 XML，如上一節所示，將它轉換成 HTML 表格會顯示在瀏覽器中：  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 XSLT 轉換成 HTML 表會顯示每個表格標題以及資料錄集的欄位產生 ADO Save 方法的 XML 資料流。 資料表標題和資料列也會指派不同的字型和色彩。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
