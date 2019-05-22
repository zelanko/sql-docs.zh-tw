---
title: 'Sql: relationship (SQLXML 4.0) 指定 sql: inverse 屬性 |Microsoft Docs'
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d8a6390ded6250355936dbef29051f76be14266
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65980697"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>針對 sql:relationship 指定 sql:inverse 屬性 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Sql: inverse**屬性才有用的 XSD 結構描述在使用時才用於大量載入或由 updategram 所。 **Sql: inverse**上，可以指定屬性 **\<sql: relationship >** 項目。 在 Updategram 中，Updategram 邏輯會解譯結構描述，以便判斷 Updategram 作業所更新的資料表和資料行。 在結構描述中指定的父子式關聯性會判斷修改記錄 (插入或刪除) 的順序。  
  
 如果您有 XSD 結構描述，而且其父子式關聯性是以對應資料庫資料行之間主索引鍵/外部索引鍵關聯性的反向順序所指定，則插入或刪除 Updategram 作業將會由於主索引鍵/外部索引鍵違規而失敗。 在此情況下， **sql: inverse**指定屬性 (**sql: inverse ="true"**) 中 **\<sql: relationship >** 項目和 updategram 邏輯反向的結構描述中指定它的父子式關聯性的解譯方式。  
  
 **Sql: inverse**屬性接受布林值 (0 = false,1 = true)。 可接受的值為 0、1、true 和 false。  
  
 工作的範例使用**sql: inverse**註解，請參閱[在 Updategram 中指定註解式對應結構描述](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [關聯性使用 sql: relationship 指定&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
