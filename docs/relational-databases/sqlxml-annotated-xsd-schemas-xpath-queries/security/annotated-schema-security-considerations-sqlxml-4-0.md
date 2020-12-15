---
title: " (SQLXML) 的批註式架構安全性考慮"
description: 瞭解在 SQLXML 4.0 中使用批註式架構的安全性指導方針。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 635c32709e8ac0a97dfe669dbbba104dbb179197
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439605"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>註解式結構描述安全性考量 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  下面是使用註解式結構描述的安全性指導方針：  
  
-   請避免在對應結構描述中使用預設的對應。 預設對應會在產生的 XML 文件中公開資料庫資訊 (資料表和資料行名稱)，因為根據預設，元素名稱會對應到資料表名稱，而屬性名稱則對應到資料行名稱。 因此，看到 XML 文件的任何使用者都可以存取資料庫中的資料表和資料行資訊，因此暴露潛在的安全性風險。 為避免此風險，請在結構描述中指定任意的元素和屬性名稱，並使用註解將其明確地對應到資料表和資料行。 如需有關在建立 XSD 架構時使用預設對應的詳細資訊，請參閱 [&#40;SQLXML 4.0&#41;的 Xsd 元素和屬性與資料表和資料行的預設對應 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)。  
  
-   使用註解指定的明確對應會公開資料庫資訊 (例如資料表名稱和資料行名稱)。 因此，您可能不會想要公開地提供這些結構描述。  
  
-   某些查詢（例如針對使用遞迴的對應架構所指定的查詢 (使用 **最大深度** 注釋設定為較高的值）) 可能需要較長的時間才能執行。 您可以設定命令逾時屬性 (（以秒為單位），選擇性地指定超時限制（以秒為單位）) 。 例如：  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SQLXML 4.0 中的註解式 XSD 結構描述](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
