---
title: "將 XSD 資料型別對應到 XPath 資料類型 (SQLXML 4.0) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19ce96f9e7c7731b669f5186a1b038bade09646e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>將 XSD 資料類型對應到 XPath 資料類型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]當 XPath 查詢針對 XSD 結構描述執行，而且 XSD 類型會指定在**xsd: type**屬性，XPath 會使用在處理查詢時指定的資料類型。  
  
 節點的 XPath 資料類型衍生自結構描述中的 XSD 資料類型，如下表所示  (EmployeeID 節點用於提供說明)。  
  
|XSD 資料類型|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|SQL Server<br /><br /> 所使用的轉換|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**無**<br /><br /> **bin.base64bin.hex**|**不適用**|無<br /><br /> EmployeeID|  
|**布林**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal、 整數、 浮點數、 位元組、 short、 int、 long、 float、 double、 unsignedByte、 unsignedShort、 unsignedInt、 unsignedLong**|**數字、 int、 float、 i1、 i2、 i4、 i8、 r4、 r8ui1、 ui2、 ui4、 ui8**|**數字**|CONVERT(float(53), EmployeeID)|  
|**識別碼、 idref、 idrefsentity、 entities、 標記法、 nmtoken、 nmtokens DateTime、 字串、 AnyURI**|**id、 idref、 idrefsentity、 實體、 列舉、 標記法、 nmtoken、 nmtokens、 char、 dateTime、 dateTime.tz、 字串、 uri、 uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**不適用 （沒有任何資料類型相當於 fixed14.4 XDR 資料類型的 xpath。）**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
