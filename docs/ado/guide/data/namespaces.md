---
description: 命名空間
title: 命名空間 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: rothja
ms.author: jroth
ms.openlocfilehash: 03d70d1e5df026e13e23c9759462f53114f4d2af
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980259"
---
# <a name="namespaces"></a>命名空間
ADO 中的 XML 持續性格式會使用下列四個命名空間。  
  
## <a name="remarks"></a>備註  
 ADO 中的 XML 持續性格式會使用下列四個命名空間。  
  
|前置詞|描述|  
|------------|-----------------|  
|s|指的是包含元素和屬性的 "XML-Data" 命名空間，這些專案和屬性定義了目前記錄集的架構。|  
|dt|參考資料類型定義規格。|  
|rs|參考命名空間，其中包含 ADO 記錄集屬性和屬性專屬的元素和屬性。|  
|z|參考目前資料列集的架構。|  
  
 用戶端不應將自己的標記新增至這些命名空間，如規格所定義。 例如，用戶端不應該將命名空間定義為 "urn：架構-microsoft .com： rowset"，然後寫出像是 "rs： MyOwnTag" 的內容。 若要深入瞭解命名空間，請參閱 [XML 建議的 W3C 命名空間](http://www.w3.org/TR/REC-xml-names/)。  
  
> [!IMPORTANT]
>  架構標記的識別碼必須是 "RowsetSchema"，而用來參考目前資料列集架構的命名空間必須指向 "#RowsetSchema"。  
  
 請注意命名空間的前置詞（冒號和等號之間的部分）是任意的。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 只要整個 XML 檔都使用此名稱，使用者就可以將此定義為任何名稱。 ADO 一律會寫出 "s"、"rs"、"dt" 和 "z"，但是這些前置詞名稱不會硬式編碼到載入元件中。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](./persisting-records-in-xml-format.md)