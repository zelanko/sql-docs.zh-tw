---
title: NULL 處理 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1a6da64b6a626da7dcdc3ff8b29c9e291b8684b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160038"
---
# <a name="null-handling-sqlxml-40"></a>NULL 處理 (SQLXML 4.0)
  XML 語法表示 NULL 不存在  (例如，如果屬性或元素值為 NULL，該屬性或元素就會從 XML 文件中消失)。在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 中，`updg:nullvalue` 屬性允許針對元素或屬性值指定 NULL。  
  
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
  
 當參數傳遞到 Updategram 時，NULL 可以當做參數值傳遞。 這可以透過指定 `nullvalue` 區塊中的 `<updg:header>` 屬性完成。 如需範例，請參閱[傳遞到 Updategram 的參數&#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
