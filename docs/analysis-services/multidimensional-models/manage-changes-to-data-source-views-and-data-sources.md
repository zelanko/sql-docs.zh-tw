---
title: "管理資料來源檢視和資料來源變更 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data sources
- modifying data source views
- data source views [Analysis Services], schema updates
- data sources [Analysis Services], schema updates
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b1913d392467f4ba78976d9ab73919e7ac06051
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>管理對資料來源檢視及資料來源所做的變更
  當結構描述產生精靈重新執行時，會重新使用它在原始產生所使用的相同資料來源和資料來源檢視。 如果您加入資料來源或資料來源檢視，精靈不會使用它。 如果您在初始產生之後刪除原始資料來源或資料來源檢視，您必須從頭開始執行精靈。 精靈中所有先前的設定也會被刪除。 下次您執行結構描述產生精靈時，對於基礎資料庫中任何繫結到已刪除之資料來源或資料來源檢視的現有物件，將視同使用者建立的物件來處理。  
  
 如果資料來源檢視在產生時不會反映基礎資料庫的實際狀態，則當「結構描述產生精靈」產生主題領域資料庫的結構描述時，可能會遇到錯誤。 例如，如果資料來源檢視指定資料行的資料類型為 **int**，但是該資料行的資料類型實際上是 **string**，則「結構描述產生精靈」會將外部索引鍵的資料類型設為 **INT** ，以符合此資料來源檢視，但是當它建立關聯性時會失敗，因為實際資料類型是 **string**。  
  
 相反地，如果您將資料來源連接字串，變更為與前一次產生不同的資料庫，則不會產生錯誤。 這時會使用新資料庫，且先前的資料庫不會產生任何變更。  
  
## <a name="see-also"></a>請參閱＜  
 [了解累加式產生](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  

