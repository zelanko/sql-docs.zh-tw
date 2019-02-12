---
title: NULL 處理 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 253e29ffb6b0723d672fdbf4de8a3cd6aff334d4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015589"
---
# <a name="null-handling-sqlxml-40"></a>NULL 處理 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 語法表示 NULL 不存在  (例如，如果屬性或元素值為 NULL，該屬性或元素就會從 XML 文件中消失)。在  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML， **updg: nullvalue**屬性可讓針對項目或屬性的值指定 NULL。  
  
 例如，下列 updategram 可確保**標題**值，將此連絡人**ContactID** 64 是 NULL，，然後更新**標題**值為"Mr." 。  
  
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
  
 當參數傳遞到 Updategram 時，NULL 可以當做參數值傳遞。 這是藉由指定**nullvalue**屬性中 **\<updg:header >** 區塊。 如需範例，請參閱[傳遞到 Updategram 的參數&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
