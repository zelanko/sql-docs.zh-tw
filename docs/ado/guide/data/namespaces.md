---
title: 命名空間 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 419d11660d88f102cfa92628f4ee16fb89d8c422
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272087"
---
# <a name="namespaces"></a>命名空間
在 ADO 中的 XML 持續性格式會使用下列四個命名空間。  
  
## <a name="remarks"></a>備註  
 在 ADO 中的 XML 持續性格式會使用下列四個命名空間。  
  
|Prefix|描述|  
|------------|-----------------|  
|s|是指 「 XML 資料 」 命名空間包含的項目和目前資料錄集的結構描述定義的屬性。|  
|dt|參考的資料型別定義的規格。|  
|rs|參考的命名空間包含的項目和屬性特定的 ADO 資料錄集的屬性和屬性。|  
|z|參考目前資料列集的結構描述。|  
  
 用戶端應該不自己將標記加入至這些命名空間，如規格所定義。 比方說，用戶端不應定義為命名空間 」 描述 urn:-microsoft-com:rowset 」 並接著寫出項目，例如"rs: MyOwnTag。 」 若要深入了解命名空間，請參閱[XML 建議事項中的 W3C 命名空間](http://www.w3.org/TR/REC-xml-names/)。  
  
> [!IMPORTANT]
>  結構描述的標記 ID 必須是"RowsetSchema 」，而且用來參考目前資料列集的結構描述的命名空間必須指向 「 #RowsetSchema。 」  
  
 請注意，前置詞的命名空間，冒號和等號之間的部分 — 是任意的。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 使用者可以定義為任何名稱，只要整個 XML 文件便固定使用此名稱。 ADO 永遠會寫出"s，""rs 」，「 dt 」，"z，"但這些前置詞名稱不是硬式編碼成載入元件。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
