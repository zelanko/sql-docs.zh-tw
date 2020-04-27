---
title: 關聯性暫存資料表 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b5cc194306a4baecb2c5fa5478bf4733d1386af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67284986"
---
# <a name="relationship-staging-table-master-data-services"></a>關聯性暫存資料表 (Master Data Services)
  使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中的關聯性暫存資料表 (stg.name_Relationship) 來依據成員之間的必要關聯性變更成員在明確階層中的位置。  
  
##  <a name="table-columns"></a><a name="TableColumns"></a>資料表資料行  
 下表說明關聯性暫存資料表中各欄位的用途。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**識別碼**|自動指派的識別碼。 請勿在此欄位中輸入值。 如果尚未處理批次，這個欄位是空白。|  
|**RelationshipType**<br /><br /> 必要|所設定的關聯性類型。 可能的值包括：<br /><br /> **1**：父系<br /><br /> **2**：同層級 (在相同層級)|  
|**ImportStatus_ID**<br /><br /> 必要|匯入程序的狀態。 可能的值包括：<br /><br /> **0**：您用來指定記錄已備妥，可供暫存。<br /><br /> **1**：自動指派，表示記錄的暫存處理序已成功。<br /><br /> **2**：自動指派，表示記錄的暫存處理序已失敗。|  
|**Batch_ID**<br /><br /> 只有 Web 服務需要|自動指派的識別碼，可用來將暫存的記錄分組。 批次中的所有成員都會被指派這個識別碼，這個識別碼會顯示在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面的 **[識別碼]** 欄中。<br /><br /> 如果尚未處理批次，這個欄位是空白。|  
|**BatchTag**<br /><br /> 必要項，只有 Web 服務不需要|批次的唯一名稱 (最多 50 個字元)。|  
|**HierarchyName**<br /><br /> 必要|明確階層名稱。 每一個合併成員只能屬於一個階層。|  
|**ParentCode**<br /><br /> 必要|若是父子式關聯性，即為分葉子成員或合併子成員之父系的合併成員代碼。<br /><br /> 若是同層級關聯性，即為其中一個同層級的代碼。|  
|**ChildCode**<br /><br /> 必要|若是父子式關聯性，即為子系的合併成員或分葉成員代碼。<br /><br /> 若是同層級關聯性，即為其中一個同層級的代碼。|  
|**排序次序**<br /><br /> 選擇性|一個整數，代表此成員相對於父系底下其他成員的順序。 每個子成員都應該有一個唯一識別碼。|  
|**錯誤碼**|顯示錯誤碼。 若要查詢 **ImportStatus_ID** 為 **2**的所有記錄，請參閱 [暫存處理序錯誤 &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [使用暫存進程 &#40;Master Data Services 來移動明確階層成員&#41;](add-update-and-delete-data-master-data-services.md)   
 [資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [查看暫存進程期間發生的錯誤 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [暫存處理序錯誤 &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
