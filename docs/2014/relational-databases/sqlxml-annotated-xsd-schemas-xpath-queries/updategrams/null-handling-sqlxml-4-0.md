---
title: NULL 處理 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
ms.openlocfilehash: 59110e6686307e9555355fb72fefdbf6099bbc69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63060107"
---
# <a name="null-handling-sqlxml-40"></a>NULL 處理 (SQLXML 4.0)
  XML 語法表示 NULL 不存在  (例如，如果屬性或項目值是 NULL，該屬性或項目不存在將 XML 文件。)在  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML、`updg:nullvalue`屬性可讓針對項目或屬性的值指定 NULL。  
  
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
  
  
