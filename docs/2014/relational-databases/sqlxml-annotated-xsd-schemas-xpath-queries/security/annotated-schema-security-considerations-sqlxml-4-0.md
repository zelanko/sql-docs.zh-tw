---
title: 註解式結構描述安全性考量 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4834255ba7f6024c484c8142ccfb4d18a9e6f44c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325668"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>註解式結構描述安全性考量 (SQLXML 4.0)
  下面是使用註解式結構描述的安全性指導方針：  
  
-   請避免在對應結構描述中使用預設的對應。 預設對應會在產生的 XML 文件中公開資料庫資訊 (資料表和資料行名稱)，因為根據預設，元素名稱會對應到資料表名稱，而屬性名稱則對應到資料行名稱。 因此，看到 XML 文件的任何使用者都可以存取資料庫中的資料表和資料行資訊，因此暴露潛在的安全性風險。 為避免此風險，請在結構描述中指定任意的元素和屬性名稱，並使用註解將其明確地對應到資料表和資料行。 如需使用預設對應，當您建立 XSD 結構描述的詳細資訊，請參閱 <<c0> [ 預設對應的 XSD 項目和屬性對資料表和資料行&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)。</c0>  
  
-   使用註解指定的明確對應會公開資料庫資訊 (例如資料表名稱和資料行名稱)。 因此，您可能不會想要公開地提供這些結構描述。  
  
-   某些查詢 (例如，根據對應結構描述利用遞迴指定的查詢 (透過將 `max-depth` 註解設定為較高的值指定)) 執行時間可能更久。 您可以選擇性地指定逾時限制，藉由設定命令逾時屬性 （以秒為單位）。 例如：  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SQLXML 4.0 中的註解式 XSD 結構描述](../../sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
