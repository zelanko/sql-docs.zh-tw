---
title: "OData 來源屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 64e297a37c3b6449551968b5788f8c2c0ddd4ab6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source-properties"></a>OData 來源屬性
當您以滑鼠右鍵按一下**OData 來源**資料流程中按一下**屬性**，查看屬性**OData 來源**元件**屬性**視窗。  

## <a name="properties"></a>屬性 
|屬性|說明|  
|-|-|  
|CollectionName|若要從 OData 服務擷取集合的名稱。 當 **UseResourcePath** 為 False 時，便會使用 **CollectionName** 屬性。<br /><br /> 這個屬性是 expressionable，可讓您在執行階段設定的值。 不過，如果集合的中繼資料不符合在設計階段的中繼資料，驗證就會發生錯誤，導致資料流程執行失敗。|  
|DefaultStringLength|這個值會針對沒有最大長度的字串資料行指定預設長度。<br /><br /> **預設值：** 4000|  
|查詢|OData 查詢參數。 這個屬性是 expressionable，而且可以在執行階段設定。|  
|ResourcePath|當您需要指定完整資源路徑時請使用這個屬性，而不要選取集合名稱。 當 **UseResourcePath** 為 True 時，便會使用這個屬性。|  
|CollectionName|當設定為 True 時， **ResourcePath** 值會附加至基底 URL，以判斷 OData 摘要位置。 當設定為 False 時，便會使用 **CollectionName** 值。<br /><br /> **預設值：** False|  
  
## <a name="see-also"></a>另請參閱
[OData 來源](odata-source.md)

