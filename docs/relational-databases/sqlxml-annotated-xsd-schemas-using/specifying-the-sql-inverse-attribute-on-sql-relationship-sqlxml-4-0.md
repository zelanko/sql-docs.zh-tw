---
title: Set sql： sql： relationship (SQLXML) 的反向屬性
description: 瞭解如何在 sql： relationship 元素上使用 sql：反向屬性，以指定 updategram 作業中的資料庫資料行之間的關聯性。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- bulk load [SQLXML]
- inverse attribute
- relationships [SQLXML], inverse orders
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- updategrams [SQLXML], relationships
- sql:inverse
ms.assetid: 08904cbd-9c86-493d-90c3-f5e1d13ce59d
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b714a70cb3d537d3f9859945b5fdee6842aa5d58
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479339"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>針對 sql:relationship 指定 sql:inverse 屬性 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  **Sql：反向** 屬性只有在 XSD 架構用於大量載入或 updategram 時才有用。 您可以在元素上指定 **sql：反向** 屬性 **\<sql:relationship>** 。 在 Updategram 中，Updategram 邏輯會解譯結構描述，以便判斷 Updategram 作業所更新的資料表和資料行。 在結構描述中指定的父子式關聯性會判斷修改記錄 (插入或刪除) 的順序。  
  
 如果您有 XSD 結構描述，而且其父子式關聯性是以對應資料庫資料行之間主索引鍵/外部索引鍵關聯性的反向順序所指定，則插入或刪除 Updategram 作業將會由於主索引鍵/外部索引鍵違規而失敗。 在這種情況下， **sql：反向** 屬性是在元素中指定 (**sql：反向 = "true"**) **\<sql:relationship>** ，而 updategram 邏輯則會反轉架構中所指定之父子式關聯性的解讀。  
  
 **Sql：反向** 屬性採用布林值 (0 = false，1 = true) 。 可接受的值為 0、1、true 和 false。  
  
 如需使用 **sql：反向** 注釋的實用範例，請參閱 [在 Updategram 中指定批註式對應架構](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 sql： relationship 指定關聯性 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
