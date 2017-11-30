---
title: "使用快照集 (Web 入口網站) | Microsoft Docs"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ae20556-e243-4a60-b076-9fd9e82c7355
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7498112d3822d18976ea6482c6014ce7bc69435f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="working-with-snapshots-web-portal"></a>使用快照集 (入口網站)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

您可以控制是否要為報表建立快照集，方法是選取報表的**省略符號 (...)**，並選取 [管理]，然後選取 [快取] 或 [記錄快照集]。  
  
> [!NOTE]
> 需要啟動 SQL Server Agent 服務。  
   
您可以建立快取快照集，以允許更快速地載入特定執行屬性。 您也可以使用記錄快照集來擷取時間點。  
  
## <a name="creating-a-cache-snapshot"></a>建立快取快照集  
  
您可以透過下列方式建立快照集。  
  
![ssRSWebPortal-report-caching4](../reporting-services/media/ssrswebportal-report-caching4.png)  
  
1.  在 [快取] 頁面上，選取 [永遠針對預先產生的快照集執行此報表] 啟用建立快照集的選項。  
  
2.  如果您想要排程週期性快照集，請選取 [依排程建立快取快照集]。 然後，您可以使用共用排程，或定義自訂排程來重新整理快照集。  
  
3.  如果您想要立即建立快取快照集，請選取 [在我按一下此頁面上的 [套用] 時建立快取快照集]。 如果您只選取這個選項，將不會重新整理快照集。  
  
## <a name="create-modify-and-delete-history-snapshots"></a>建立、修改及刪除記錄快照集  
  
若要使用記錄快照集，請管理報表，並選取 [記錄快照集]。  
  
使用 [記錄快照集] 頁面來檢視產生和儲存一段時間的報表快照集。 依據在報表伺服器上設定的選項，記錄可能只包含最近的快照集。  
  
報表記錄一定是在資源報表的內容中提供檢視的。 您無法在某個位置中檢視報表伺服器上所有報表的記錄。  
  
若要產生記錄快照集，報表必須可以自動執行 (亦即它必須使用預存認證；參數化的報表必須包含所有參數的預設參數值)。 可以手動或以排程作業來產生報表記錄。 報表的記錄屬性決定建立報表記錄的方式。  
  
![ssRSWebPortal-historysnapshots1](../reporting-services/media/ssrswebportal-historysnapshots1.png)  
   
1.  若要建立記錄快照集，請選取 [+ 新增記錄快照集]。 這會處理報表並將一個項目加入清單。  
  
2.  您可以移至設定以定義排程和保留原則。  
  
3.  您可以選取並檢視記錄快照集。 報表記錄中顯示的快照集只能以建立日期和時間來區分。 沒有視覺指示可以區分快照集是回應排程而建立或是手動作業所建立。  
  
### <a name="schedule-and-settings"></a>排程及設定  
  
選取 [排程及設定] 會提供其他選項，以排程及控制所建立之快照集的保留期。  
  
![ssRSWebPortal-historysnapshots2](../reporting-services/media/ssrswebportal-historysnapshots2.png)  
   
您可以選擇為快照集建立排程以開始建立。 您也可以防止其他人員建立新的快照集。 取消核取 [允許人員手動建立快照集] 將會停用 [+ 新增記錄快照集] 按鈕。  
  
您也可以定義要保留快照集的方式。  
  
**也將快取快照集儲存至報表記錄**  
  
選取此選項，將根據報表執行屬性所產生的報表快照集，複製到報表記錄。 可以將報表執行屬性設定為，從產生的快照集來執行報表。 設定此報表記錄屬性，就可以將所有長期產生的報表快照集複本，放入報表記錄中作為保存。

## <a name="next-steps"></a>後續的步驟

[入口網站](../reporting-services/web-portal-ssrs-native-mode.md)  
[使用分頁報表](working-with-paginated-reports-web-portal.md)  
[使用共用資料集](../reporting-services/work-with-shared-datasets-web-portal.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
