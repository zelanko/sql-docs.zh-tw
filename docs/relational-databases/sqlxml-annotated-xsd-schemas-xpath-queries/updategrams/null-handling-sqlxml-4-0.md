---
title: Null 處理（SQLXML）
description: 瞭解如何在 SQLXML 4.0 updategram 中，使用 updg： nullvalue 屬性來指定 Null 屬性或元素。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57a0517bc698d2969d1ee1808cb52769fa8ef4ae
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790572"
---
# <a name="null-handling-sqlxml-40"></a>NULL 處理 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XML 語法表示 NULL 不存在  （例如，如果屬性或專案值為 Null，則 XML 檔中不存在該屬性或元素）。在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 中， **updg： nullvalue**屬性可為元素或屬性值指定 Null。  
  
 例如，下列 updategram 可確保**ContactID**為64之連絡人的**標題**值為 Null，然後將**標題**值更新為「Mr」。 。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 當參數傳遞到 Updategram 時，NULL 可以當做參數值傳遞。 這是藉由在區塊中指定**nullvalue**屬性來完成 **\<updg:header>** 。 如需範例，請參閱[將參數傳遞至 updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
