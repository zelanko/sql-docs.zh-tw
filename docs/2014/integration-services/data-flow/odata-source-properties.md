---
title: OData 來源屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fbae9e97e99223665e6d89d9e8c1a2bce3e48a26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62901197"
---
# <a name="odata-source-properties"></a>OData 來源屬性
  當您以滑鼠右鍵按一下資料流程中的 [OData 來源]**** 並按一下 [屬性]**** 時，您將會看到 [OData 來源]**** 元件的屬性出現在 [屬性]**** 視窗中。  
  
|||  
|-|-|  
|屬性|描述|  
|CollectionName|您想要從 OData 服務擷取的集合名稱。 當 **UseResourcePath** 為 False 時，便會使用 **CollectionName** 屬性。<br /><br /> 此屬性具有運算式功能，可在執行階段設定值。 不過，如果集合的中繼資料不符合在設計階段所使用的中繼資料，將會發生驗證錯誤，導致資料流程執行失敗。|  
|DefaultStringLength|這個值會針對沒有最大長度的字串資料行指定預設長度。<br /><br /> **預設值：** 4000|  
|查詢|OData 查詢參數。 此屬性具有運算式功能，而且可在執行階段設定。|  
|ResourcePath|當您需要指定完整資源路徑時請使用這個屬性，而不要選取集合名稱。 當 **UseResourcePath** 為 True 時，便會使用這個屬性。|  
|CollectionName|當設定為 True 時， **ResourcePath** 值會附加至基底 URL，以判斷 OData 摘要位置。 當設定為 False 時，便會使用 **CollectionName** 值。<br /><br /> **預設：** False|  
  
  
