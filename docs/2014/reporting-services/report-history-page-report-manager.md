---
title: 報表記錄頁面 （報表管理員） |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 0b0841e031ee1a98f4f678406f790996a709e90f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104474"
---
# <a name="report-history-page-report-manager"></a>報表記錄頁面 (報表管理員)

使用 [報表記錄] 頁面來檢視產生和儲存一段時間的報表快照集。 依據在報表伺服器上設定的選項，報表記錄可能只包含最近的快照集。  
  

報表記錄一定是在資源報表的內容中提供檢視的。 您無法在某個位置中檢視報表伺服器上所有報表的記錄。  
  
若要產生報表記錄，報表必須可以自主式執行 (亦即它必須使用預存認證；參數化的報表必須包含所有參數的預設參數值)。 可以手動或以排程作業來產生報表記錄。 報表的記錄屬性決定建立報表記錄的方式。  
  
按一下報表記錄快照集即可檢視該快照集。 報表記錄中顯示的快照集只能以建立日期和時間來區分。 沒有視覺指示可以區分快照集是回應排程而建立或是手動作業所建立。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-report-history-page"></a>若要開啟報表記錄頁面  
  
1.  開啟報表管理員，然後找出您想要檢視報表快照集的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[檢視報表記錄]**。  
  
## <a name="options"></a>選項。  
 **刪除**  
 按一下即可刪除一個或多個快照集。 在按一下 **[刪除]** 之前，請先選取要刪除之快照集旁邊的核取方塊。  
  
 **新的快照集**  
 按一下即可將快照集加入至報表記錄。 只有在報表的記錄屬性頁面上選擇 **[允許手動建立記錄]** 選項時，才能使用此按鈕。  
  
 **最後執行**  
 顯示建立快照集的日期和時間。 按一下描述以檢視特殊快照集。  
  
 **大小**  
 顯示報表定義加報表中資料的大小。 此值指出報表定義和資料使用報表伺服器資料庫中多少空間。 轉譯報表的大小 (包括格式) 實際上會比較大。 括號中指出的總大小是目前報表的報表記錄中之所有快照集大小的總和。  
  
## <a name="see-also"></a>另請參閱  
 [檢視或刪除報表記錄&#40;報表管理員&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [將快照集加入報表記錄 &#40;報表管理員&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [一般屬性頁面，報表 &#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [快照集選項屬性頁面&#40;報表管理員&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)