---
title: "XSLT 轉換 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7fb8a2fc948c7793ed07076f338c230350d6abb1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="xslt-transformations"></a>XSLT 轉換
XSLT 可以套用至所產生的 XML，將它轉換成另一種格式。 了解在 ADO 中的 XML 格式，可以協助開發可以將它轉換成更方便使用的表單的 XSLT 範本。  
  
 例如，您知道資料錄集的每個資料列會儲存為 z： 資料列內的項目 rs： 資料元素。 同樣地，每個資料錄集的欄位會儲存為此元素的屬性值配對。  
  
## <a name="remarks"></a>備註  
 下列的 XSLT 指令碼可以套用至要顯示在瀏覽器中顯示上一節中將它轉換成 HTML 表格的 XML:  
  
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
  
 XSLT 轉換 XML 資料流 ADO 儲存方法所產生以 HTML 表格會顯示每個表格標題以及資料錄集的欄位。 資料表標題和資料列也會指派不同的字型和色彩。  
  
## <a name="see-also"></a>請參閱＜  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
