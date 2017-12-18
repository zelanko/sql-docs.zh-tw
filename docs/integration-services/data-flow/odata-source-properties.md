---
title: "OData 來源屬性 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ff5a45fff7cc967f8fbec8d07926fe0c9fe3a83
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="odata-source-properties"></a>OData 來源屬性
當您以滑鼠右鍵按一下資料流程中的 [OData 來源] 並按一下 [屬性] 時，您會看到 [OData 來源] 元件的屬性出現在 [屬性] 視窗中。  

## <a name="properties"></a>屬性 
|屬性|說明|  
|-|-|  
|CollectionName|要從 OData 服務擷取的集合名稱。 當 **UseResourcePath** 為 False 時，便會使用 **CollectionName** 屬性。<br /><br /> 此屬性具有運算式功能，可在執行階段設定值。 不過，如果集合的中繼資料不符合存在於設計階段的中繼資料，則會發生驗證錯誤，導致資料流程執行失敗。|  
|DefaultStringLength|這個值會針對沒有最大長度的字串資料行指定預設長度。<br /><br /> **預設值：** 4000|  
|查詢|OData 查詢參數。 此屬性具有運算式功能，而且可在執行階段設定。|  
|ResourcePath|當您需要指定完整資源路徑時請使用這個屬性，而不要選取集合名稱。 當 **UseResourcePath** 為 True 時，便會使用這個屬性。|  
|CollectionName|當設定為 True 時， **ResourcePath** 值會附加至基底 URL，以判斷 OData 摘要位置。 當設定為 False 時，便會使用 **CollectionName** 值。<br /><br /> **預設值：** False|  
  
## <a name="see-also"></a>另請參閱
[OData 來源](odata-source.md)
