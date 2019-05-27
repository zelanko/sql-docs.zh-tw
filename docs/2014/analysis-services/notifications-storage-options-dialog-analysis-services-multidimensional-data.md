---
title: 通知 （儲存選項對話方塊） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.notifications.f1
ms.assetid: 5675cdbf-bfaa-4b6e-b716-31b8e9da72b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23845118c4c202db781fe325c4afc2402ceee271
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072197"
---
# <a name="notifications-storage-options-dialog-box-analysis-services---multidimensional-data"></a>通知 (儲存選項對話方塊) (Analysis Services - 多維度資料)
  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [儲存選項] 對話方塊中，使用 [通知] 索引標籤，即可設定通知方法以及維度、Cube、量值群組或資料分割的相關設定。  
  
> [!NOTE]  
>  在您修改這些設定之前，必須先熟悉儲存模式與主動式快取功能。 如需詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**儲存模式**|選取用於物件的儲存模式。<br /><br /> **MOLAP**<br /> 物件使用多維度 OLAP (MOLAP) 儲存。<br /><br /> **HOLAP**<br /> 物件使用混合式 OLAP (HOLAP) 儲存。<br /><br /> **ROLAP**<br /> 物件使用關聯式 OLAP (ROLAP) 儲存。|  
|**啟用主動式快取**|啟用主動式快取。<br /><br /> 注意:如果未選取此選項，所有選項除了**儲存模式**會停用。|  
|**SQL Server**|使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 上之特定的追蹤機制，來識別物件之基礎資料表的變更。|  
|**指定追蹤資料表**|指定要為物件追蹤的基礎資料表，然後鍵入以分號 (;) 字元分隔的資料表清單，或按一下省略符號按鈕 (**...**) 即可開啟 [關聯式物件] 對話方塊，然後選擇要追蹤的資料表。 如需詳細資訊，請參閱[關聯式物件對話方塊 &#40;Analysis Services - 多維度資料&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 如果未選取此選項，則只要符合特定需求，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 就會嘗試決定要為物件追蹤的基礎資料表清單。 如需這些需求的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**用戶端起始**|選取即可使用 XML for Analysis (XMLA) 命令 `NotifyTableChange`，來識別物件之基礎資料表的變更。 如果您計畫使用以用戶端為基礎的通知處理，一般會選取此選項。|  
|**指定追蹤資料表**|選取即可指定要為物件追蹤的基礎資料表，然後鍵入以分號 (;) 字元分隔的資料表清單，或按一下省略符號按鈕 (**...**) 即可開啟 [關聯式物件] 對話方塊，然後選擇要追蹤的資料表。 如需詳細資訊，請參閱[關聯式物件對話方塊 &#40;Analysis Services - 多維度資料&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 如果未選取此選項，則只要符合特定需求，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 就會嘗試決定要為物件追蹤的基礎資料表清單。 如需這些需求的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**排程的輪詢**|使用輪詢機制來識別在物件的基礎資料表上執行一系列查詢的變更。|  
|**輪詢間隔**|指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行輪詢方格中所定義的輪詢查詢和處理查詢之前，應先經過的時間間隔和單位。|  
|**啟用累加式更新**|依據一組專門設計來識別其他資料的輪詢和處理查詢，以累加的方式更新物件的 MOLAP 快取。 如果選取此選項，輪詢查詢就會與資料來源檢視中的資料表識別碼相關聯。 接著，使用處理查詢來比較輪詢查詢目前的值與先前執行之輪詢查詢的儲存值，以識別變更。<br /><br /> 如果未選取此選項，則會完整更新 MOLAP 快取。 輪詢查詢是用來識別已發生的變更，且不需要有處理查詢或資料表識別碼。|  
|**輪詢方格**|包含 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用的輪詢查詢、處理查詢和資料表識別碼，以輪詢資料來源和識別物件之基礎資料表的變更。 方格包含下列資料行：<br /><br /> **排程輪詢**：依輪詢間隔鍵入要執行的單一查詢以識別物件的變更，或按一下省略符號按鈕 (**...**) 即可開啟 [建立輪詢查詢] 對話方塊，並定義單一查詢。 如需詳細資訊，請參閱[建立輪詢查詢對話方塊 &#40;Analysis Services - 多維度資料&#41;](create-polling-query-dialog-box-analysis-services-multidimensional-data.md)。 如果選取 [啟用累加式更新]，則輪詢查詢應傳回會識別加入 [資料表] 中所識別資料表的最後一筆記錄的值。 如果未選取 [啟用累加式更新]，則輪詢查詢應傳回會識別資料表中之目前記錄數目的值。<br /><br /> **處理查詢**：依輪詢間隔鍵入要執行的查詢，即可從 [資料表] 識別的資料表中擷取新記錄，或按一下省略符號按鈕 (**...**) 即可開啟 [建立處理查詢] 對話方塊，並定義查詢。 如需詳細資訊，請參閱[建立處理查詢對話方塊 &#40;Analysis Services - 多維度資料&#41;](create-processing-query-dialog-box-analysis-services-multidimensional-data.md)。 應該參數化查詢，以接受中的查詢所傳回的兩個參數的上一個值**輪詢查詢**和中的查詢所傳回的目前值**輪詢查詢**-，可以用來識別和擷取輪詢期間加入的記錄。 請注意，只有當選取 [啟用累加式更新] 時，才能啟用此選項。<br /><br /> **資料表**：針對 [輪詢查詢] 中追蹤最後一筆記錄的查詢，鍵入資料表的識別碼，或按一下省略符號按鈕 (**...**) 即可開啟 [尋找資料表] 對話方塊，並選取資料表。 如需詳細資訊，請參閱[尋找資料表對話方塊 &#40;Analysis Services - 多維度資料&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [儲存體選項的對話方塊&#40;Analysis Services-多維度資料&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)  
  
  
