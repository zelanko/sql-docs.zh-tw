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
manager: craigg
ms.openlocfilehash: e352a6c4d548b382d700c54cf0167fadcec8bf7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126882"
---
# <a name="namespaces"></a>命名空間
在 ADO 中的 XML 保存格式會使用下列四個命名空間。  
  
## <a name="remarks"></a>備註  
 在 ADO 中的 XML 保存格式會使用下列四個命名空間。  
  
|Prefix|描述|  
|------------|-----------------|  
|s|是指 「 XML 資料 」 命名空間包含的項目和屬性，定義目前的資料錄集的結構描述。|  
|dt|參考的資料型別定義的規格。|  
|rs|參考的命名空間包含的項目和專屬 ADO 資料錄集屬性的屬性和屬性。|  
|z|參考目前資料列集的結構描述。|  
  
 用戶端應該將它自己的標記加入這些命名空間，如規格所定義。 比方說，用戶端應該不會定義在命名空間中的"urn: schemas-microsoft-microsoft-com:rowset"，然後撰寫出類似 「 rs: MyOwnTag。 」 若要深入了解命名空間，請參閱[W3C Namespaces in XML 建議事項](http://www.w3.org/TR/REC-xml-names/)。  
  
> [!IMPORTANT]
>  結構描述標記的識別碼必須是"RowsetSchema 」，而且用來參考目前資料列集的結構描述的命名空間必須指向 「 #RowsetSchema。 」  
  
 請注意-冒號和等號之間的部分為命名空間的前置詞是任意的。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 使用者可以定義這是任何名稱，只要這個名稱固定使用整個 XML 文件。 ADO 永遠會寫出"s，""rs，""dt"，"z，"但這些前置詞名稱不是硬式編碼至載入元件。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
