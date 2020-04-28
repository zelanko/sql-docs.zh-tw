---
title: 將 XSD 資料類型對應到 XPath 資料類型（SQLXML）
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b956bf3a52b9ae14e59af770d279e8be8fec028
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257380"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>將 XSD 資料類型對應到 XPath 資料類型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  針對 XSD 架構執行 XPath 查詢，並在**xsd： type**屬性中指定 xsd 類型時，xpath 會使用處理查詢時指定的資料類型。  
  
 節點的 XPath 資料類型衍生自結構描述中的 XSD 資料類型，如下表所示  (EmployeeID 節點用於提供說明)。  
  
|XSD 資料類型|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|SQL Server<br /><br /> 所使用的轉換|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**None**<br /><br /> **base64bin. hex**|**不適用**|None<br /><br /> EmployeeID|  
|**True**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal、integer、float、byte、short、int、long、float、double、unsignedByte、unsignedShort、unsignedInt、unsignedLong**|**number、int、float、i1、i2、i4、i8、r4、r8ui1、ui2、ui4、ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**id、idref、idrefsentity、entities、notation、nmtoken、nmtokens、DateTime、string、AnyURI**|**id、idref、idrefsentity、entities、enumeration、notation、nmtoken、nmtokens、char、dateTime、dateTime.tz、string、uri、uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**不適用 (在 XPath 中沒有相當於 fixed14.4 XDR 資料類型的資料類型。)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
