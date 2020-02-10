---
title: 新增、更新和刪除資料（Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b6295ead-bd2f-49dd-8756-35c6afb59648
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2212e7424f22ecca2619ef7215bf94b0dbb62875
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054267"
---
# <a name="add-update-and-delete-data-master-data-services"></a>加入、更新及刪除資料 (Master Data Services)
  您可以將大量資料加入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]的模型中，也可對模型中的資料進行大量變更。  
  
 **必要條件**  
  
-   您必須具備權限，才能將資料插入 \< 資料庫的 stg.\<名稱>_Leaf、stg.\<名稱>_Consolidated、stg.[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]名稱>_Relationship 資料表中。  
  
-   您必須具備權限，才能執行 \< 資料庫中的 stg.udp_\_名稱>_Leaf、stg.udp\<\_名稱>_Consolidated 或 stg.udp\<[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]名稱>_Relationship 預存程序。  
  
-   模型的狀態不得為 [已認可] ****。  
  
 **若要加入、更新和刪除資料庫中的[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]資料**  
  
1.  準備要匯入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫之適當暫存資料表中的成員，這包括為必要欄位提供值。 如需臨時表的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
    -   對於分葉成員，資料表為 stg.\<名稱>_Leaf，其中 \<名稱> 是指對應的實體。 如需必要欄位的資訊，請參閱[分葉成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   對於合併成員，資料表是 stg.\<名稱>_Consolidated。 如需必要欄位的資訊，請參閱[合併成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)。  
  
    -   對於要移動明確階層中的成員位置，資料表是 stg.\<名稱>_Relationship。 如需必要欄位的資訊，請參閱[合併成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md)。  
  
         如需在明確階層中移動成員的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
    -   使用 **ImportType** 欄位值，指定您要建立新成員、停用成員或刪除成員。 如需這些值的詳細資訊，請參閱[分葉成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md) 和[合併成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)。  
  
         如需停用及刪除成員的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
2.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並連接到您 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 Database Engine 執行個體。  
  
     如需詳細資訊，請參閱[SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md)。  
  
3.  使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [匯入和匯出精靈]，將資料匯入暫存資料表。  
  
     如需詳細資訊，請參閱＜ [SQL Server Import and Export Wizard](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)＞。  
  
4.  執行下列其中一項作業，將資料從暫存資料表載入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料表：  
  
    -   執行對應到資料所要移往之暫存資料表的暫存預存程序。  
  
         如需暫存預存程序和臨時表的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。 如需暫存預存程序之參數及程式碼範例的詳細資訊，請參閱[暫存預存程序 &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)。  
  
    -   使用主資料管理的 **整合管理** 功能。  
  
         在 [暫存批次] **** 頁面上，從下拉式清單中，選取要接收您所加入之資料的模型，然後按一下 [啟動批次] ****。 批次處理的狀態會顯示在 [狀態] **** 欄位中。 如需狀態的詳細資訊，請參閱[匯入狀態 &#40;Master Data Services&#41;](../../2014/master-data-services/import-statuses-master-data-services.md)。  
  
         ![主資料管理員中的暫存批次頁面](../../2014/master-data-services/media/mds-staging-batches.png "主資料管理員中的暫存批次頁面")  
  
         暫存程序的啟動間隔，由 ** 中的 [暫存批次間隔]**[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 設定決定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
5.  檢視暫存期間發生的錯誤。 如需詳細資訊，請參閱[在暫存進程期間發生的視圖錯誤 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)和[臨時進程錯誤 &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md)。  
  
6.  依據商務規則驗證資料。  
  
     在主資料管理員中，瀏覽至模型的 **Explorer** 功能區域，然後套用商務規則，以驗證資料。 如需詳細資訊，請參閱[根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)。 您也可以使用預存程序來驗證資料。 如需詳細資訊，請參閱 [驗證預存程序 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)。  
  
     當您從暫存資料表載入資料時，不會自動依商務規則驗證該資料。 如需何謂驗證和其發生時機的詳細資訊，請參閱[驗證 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
  
