---
title: 'Sql: relationship (SQLXML 4.0) 指定 sql: inverse 屬性 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf8d5dee0d72800c5b6250d83106cda552004536
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800790"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>針對 sql:relationship 指定 sql:inverse 屬性 (SQLXML 4.0)
  只有當 XSD 結構描述用於大量載入或由 Updategram 所使用時，`sql:inverse` 屬性才有用。 `sql:inverse`屬性可以在上指定 **\<sql: relationship >** 項目。 在 Updategram 中，Updategram 邏輯會解譯結構描述，以便判斷 Updategram 作業所更新的資料表和資料行。 在結構描述中指定的父子式關聯性會判斷修改記錄 (插入或刪除) 的順序。  
  
 如果您有 XSD 結構描述，而且其父子式關聯性是以對應資料庫資料行之間主索引鍵/外部索引鍵關聯性的反向順序所指定，則插入或刪除 Updategram 作業將會由於主索引鍵/外部索引鍵違規而失敗。 在此情況下，`sql:inverse`指定屬性 (`sql:inverse="true"`) 中 **\<sql: relationship >** 元素，而且 updategram 邏輯會反轉其指定的父子式關聯性的解譯在結構描述。  
  
 `sql:inverse` 屬性會接受布林值 (0 = false，1 = true)。 可接受的值為 0、1、true 和 false。  
  
 工作的範例使用`sql:inverse`註解，請參閱 <<c2> [ 在 Updategram 中指定註解式對應結構描述](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [關聯性使用 sql: relationship 指定&#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
