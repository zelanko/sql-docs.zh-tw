---
description: XSLT 轉換
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ae0f13b2ece4ae21e8a8f8312a561bcfd0e6c88
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758958"
---
# <a name="xslt-transformations"></a>XSLT 轉換
XSLT 可以套用至產生的 XML，以將它轉換成另一種格式。 瞭解 ADO 中的 XML 格式有助於開發可將其轉換為更容易使用的格式的 XSLT 範本。  
  
 例如，您知道記錄集的每個資料列都會儲存為 rs： data 元素內的 z:row 元素。 同樣地，記錄集的每個欄位都會儲存為這個元素的屬性-值組。  
  
## <a name="remarks"></a>備註  
 下列 XSLT 腳本可以套用至上一節所示的 XML，以將其轉換為要在瀏覽器中顯示的 HTML 資料表：  
  
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
  
 XSLT 會將 ADO Save 方法所產生的 XML 資料流程轉換成 HTML 資料表，此資料表會顯示記錄集的每個欄位以及一個資料表標題。 資料表標題和資料列也會被指派不同的字型和色彩。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](./persisting-records-in-xml-format.md)