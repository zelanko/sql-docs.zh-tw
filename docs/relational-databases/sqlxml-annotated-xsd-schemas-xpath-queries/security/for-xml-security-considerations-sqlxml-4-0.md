---
title: FOR XML 安全性考慮（SQLXML）
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 30841ac40a4870f67888debb1696de57c7e3b202
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252467"
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>FOR XML 安全性考量 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  FOR XML AUTO 模式會產生 XML 階層，在此階層中，元素名稱會對應到資料表名稱，而屬性名稱會對應到資料行名稱。 這樣會公開資料庫資料表和資料行資訊。 當您在查詢中指定資料表和資料行別名來使用 AUTO 模式 (伺服器端格式化) 時，可以隱藏資料庫資訊。 這些別名會當做產生之 XML 文件中的元素和屬性名稱來傳回。  
  
 例如，下列查詢會指定 AUTO 模式；因此，XML 格式化是在伺服器上完成：  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 在產生的 XML 文件中，這些別名是用於元素和屬性名稱：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 當您使用 NESTED 模式 (用戶端格式化) 時，只有產生之 XML 文件中的屬性才會傳回別名。 基底資料表的名稱一定會當做元素名稱傳回。 例如，下列查詢會指定 NESTED 模式。  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 在產生的 XML 文件中，基底資料表的名稱會當做元素名稱傳回，而且不會使用資料表別名：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
