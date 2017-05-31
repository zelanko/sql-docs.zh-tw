---
title: "&lt;xsd:simpleType&gt; 宣告的值 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b5ba2b2137935919d420f2eab0349a26dc8d9c87
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>&lt;xsd:simpleType&gt; 宣告的值
  下表根據所有可辨識的 XSD 簡單類型列舉，簡述適用的限制。  
  
 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 **\<xsd:simpleType>** 宣告中的 NaN 值。 伺服器將會拒絕包含 NaN 值的結構描述。  
  
|簡單類型|限制|  
|-----------------|----------------|  
|**duration**|年份部分必須在 -2^31 到 2^31-1 的範圍之間。 月、日、時、分和秒都必須在 0 到 9999 的範圍之間。 秒的部分在小數點右邊有三個額外的有效位數。|  
|**dateTime**|時區子欄位中的小時部分必須在 -14 到 +14 的接受範圍內。 年的部分必須在 1 到 9999 的範圍內。 月的部分必須在 1 到 12 的範圍內。 日的部分必須在 1 到 31 的範圍內，而且必須是有效的日曆日期。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會偵測無效的日期及傳回錯誤，例如 1974-02-31，因為 2 月沒有 31 天。<br /><br /> 第二個元件支援 100 奈秒的有效位數。 時區指示為選擇性。<br /><br /> SQL Server 2005 支援 -9999 到 9999 範圍之間的年份。 SQL Server 現在支援更具限制性的年份範圍。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。|  
|**date**|年的部分必須在 1 到 9999 的範圍內。 月的部分必須在 1 到 12 的範圍內。 日的部分必須在 1 到 31 的範圍內，而且必須是有效的日曆日期。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會偵測無效的日期及傳回錯誤，例如 1974-02-31，因為 2 月沒有 31 天。<br /><br /> SQL Server 2005 支援 -9999 到 9999 範圍之間的年份。 SQL Server 現在支援更具限制性的年份範圍。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。|  
|**gYearMonth**|年的部分必須在 -9999 到 9999 的範圍內。|  
|**gYear**|年的部分必須在 -9999 到 9999 的範圍內。|  
|**gMonthDay**|月的部分必須在 1 到 12 的範圍內。 日的部分必須在 1 到 31 的範圍內。|  
|**gDay**|日的部分必須在 1 到 31 的範圍內。|  
|**gMonth**|月的部分必須在 1 到 12 的範圍內。|  
|**decimal**|此類型的值必須符合 SQL 數值類型的格式。 此類型在內部總共可支援 38 位數，其中有 10 位數是保留給分數有效位數使用。|  
|**float**|此類型的值必須符合 SQL **real** 類型的格式。|  
|**double**|此類型的值必須符合 SQL **float** 類型的格式。|  
|**string**|此類型的值必須符合 SQL **nvarchar(max)** 類型的格式。|  
|**anyURI**|此類型值的長度不能超過 4000 個 Unicode 字元。|  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
