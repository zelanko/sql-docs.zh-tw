---
title: 命名空間 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5f28b5d593524288a755f4c9455bba39554d7bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924810"
---
# <a name="namespaces"></a>命名空間
ADO 中的 XML 持續性格式會使用下列四個命名空間。  
  
## <a name="remarks"></a>備註  
 ADO 中的 XML 持續性格式會使用下列四個命名空間。  
  
|前置詞|描述|  
|------------|-----------------|  
|s|參考「XML 資料」命名空間，其中包含定義目前記錄集之架構的元素和屬性。|  
|dt|參考資料類型定義規格。|  
|rs|參考包含 ADO 記錄集屬性和屬性特定專案和屬性的命名空間。|  
|z|參考目前資料列集的架構。|  
  
 用戶端不應該將自己的標記新增至這些命名空間，如規格所定義。 例如，用戶端不應將命名空間定義為 "urn：架構-microsoft-com：資料列集"，然後寫出類似 "rs： MyOwnTag" 的專案。 若要深入瞭解命名空間，請參閱[W3C 的 XML 命名空間建議](http://www.w3.org/TR/REC-xml-names/)。  
  
> [!IMPORTANT]
>  架構標記的識別碼必須是 "RowsetSchema"，而用來參考目前資料列集之架構的命名空間必須指向 "#RowsetSchema"。  
  
 請注意，命名空間的前置詞（冒號和等號之間的部分）是任意的。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 使用者可以將此定義為任何名稱，只要此名稱在整個 XML 檔中一致地使用即可。 ADO 一律會寫出 "s"、"rs"、"dt" 和 "z"，但是這些前置詞名稱並不會硬式編碼到載入元件中。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
