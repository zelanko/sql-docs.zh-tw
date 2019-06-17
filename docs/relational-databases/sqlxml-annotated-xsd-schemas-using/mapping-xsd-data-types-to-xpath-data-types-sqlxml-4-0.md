---
title: 將 XSD 資料類型對應到 XPath 資料類型 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f10134d4aa4d71c4471e5e3120b3f8fbd8ee1748
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980786"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>將 XSD 資料類型對應到 XPath 資料類型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  當 XPath 查詢針對 XSD 結構描述執行，而且已在指定 XSD 類型**xsd: type**屬性，XPath 會使用處理查詢時指定的資料類型。  
  
 節點的 XPath 資料類型衍生自結構描述中的 XSD 資料類型，如下表所示 (EmployeeID 節點用於提供說明)。  
  
|XSD 資料類型|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|[SQL Server]<br /><br /> 所使用的轉換|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**無**<br /><br /> **bin.base64bin.hex**|**不適用**|None<br /><br /> EmployeeID|  
|**布林**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal、 整數、 浮點數、 位元組、 short、 int、 long、 float、 double、 unsignedByte、 unsignedShort、 unsignedInt、 unsignedLong**|**數字、 int、 float、 i1、 i2、 i4、 i8、 r4，r8ui1、 ui2、 ui4、 ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**id、 idref、 idrefsentity、 實體、 標記法、 nmtoken、 nmtokens、 DateTime、 string、 AnyURI**|**id、 idref、 idrefsentity、 實體、 列舉、 標記法、 nmtoken、 nmtokens、 char、 dateTime、 dateTime.tz、 字串、 uri、 uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**不適用 （沒有資料類型中沒有相當於 fixed14.4 XDR 資料類型的 XPath。）**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
