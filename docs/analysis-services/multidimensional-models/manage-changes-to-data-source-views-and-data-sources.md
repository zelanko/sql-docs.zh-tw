---
title: 管理資料來源檢視和資料來源變更 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d1e010dece24c45a863b0c9aaf0770b1580fba4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>管理對資料來源檢視及資料來源所做的變更
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當結構描述產生精靈重新執行時，會重新使用它在原始產生所使用的相同資料來源和資料來源檢視。 如果您加入資料來源或資料來源檢視，精靈不會使用它。 如果您在初始產生之後刪除原始資料來源或資料來源檢視，您必須從頭開始執行精靈。 精靈中所有先前的設定也會被刪除。 下次您執行結構描述產生精靈時，對於基礎資料庫中任何繫結到已刪除之資料來源或資料來源檢視的現有物件，將視同使用者建立的物件來處理。  
  
 如果資料來源檢視在產生時不會反映基礎資料庫的實際狀態，則當「結構描述產生精靈」產生主題領域資料庫的結構描述時，可能會遇到錯誤。 例如，如果資料來源檢視指定資料行的資料類型為 **int**，但是該資料行的資料類型實際上是 **string**，則「結構描述產生精靈」會將外部索引鍵的資料類型設為 **INT** ，以符合此資料來源檢視，但是當它建立關聯性時會失敗，因為實際資料類型是 **string**。  
  
 相反地，如果您將資料來源連接字串，變更為與前一次產生不同的資料庫，則不會產生錯誤。 這時會使用新資料庫，且先前的資料庫不會產生任何變更。  
  
## <a name="see-also"></a>另請參閱  
 [了解累加式產生](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  
