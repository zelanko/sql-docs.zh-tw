---
title: 檢視或變更收集組排程 (SQL Server Management Studio) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: data-collection
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.dc.collectionsetprop.uploads.f1
- sql13.swb.dc.collectionsetprop.description.f1
- sql13.swb.dc.collectionsetprop.general.f1
helpviewer_keywords:
- collection sets [SQL Server], changing schedules
- schedules [SQL Server], changing collection set
- collection sets [SQL Server], viewing schedules
- schedules [SQL Server], viewing collection set
ms.assetid: 26336c98-78c5-414f-8d6a-574fc3af60c4
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d018c701915708166c7bfe7bfb29121bec5fc7f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="view-or-change-collection-set-schedules-sql-server-management-studio"></a>檢視或變更收集組排程 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來檢視或變更收集組排程。  
  
 收集模式 (快取或非快取) 可決定您要如何對排程進行變更。 快取模式會使用個別的排程來進行收集和上傳。 非快取模式會使用相同的排程來進行收集和上傳。 每一個系統資料收集組的收集模式類型如下：  
  
-   [磁碟使用量] 會使用非快取收集模式。  
  
-   **[查詢統計資料]** 會使用快取收集模式。  
  
-   **[伺服器活動]** 會使用快取收集模式。  
  
### <a name="to-view-collection-set-schedules"></a>若要檢視收集組排程  
  
1.  在 [物件總管] 中，依序展開 **[管理]** 節點、 **[資料收集]**和 **[系統資料收集組]**。  
  
2.  以滑鼠右鍵按一下收集組名稱，然後按一下 [屬性] 開啟 [[資料收集組屬性]](#CollectionSet) 對話方塊。  
  
### <a name="to-change-the-schedules-for-a-cached-mode-collection-set"></a>若要變更快取模式收集組的排程  
  
1.  在 [物件總管] 中，依序展開 **[管理]** 節點、 **[資料收集]**和 **[系統資料收集組]**。  
  
2.  以滑鼠右鍵按一下使用快取模式的收集組，例如 [查詢統計資料]，然後按一下 [屬性] 開啟 [[資料收集組屬性]](#CollectionSet) 對話方塊。  
  
3.  您可以在 **[一般]** 頁面上變更收集頻率。 若要這樣做，請遵循下列步驟：  
  
    1.  在詳細資料窗格中，按兩下針對 [收集項目] 資料表中 [收集頻率 (秒)] 資料行顯示的數字。  
  
    2.  若要增加或減少收集頻率，請輸入較低或較高的數字，然後按下 ENTER 儲存新的值。  
  
4.  若要變更收集組的現有上傳排程，請遵循下列步驟：  
  
    1.  按一下 **[上傳]** 頁面。  
  
    2.  在詳細資料窗格中，按一下 **[挑選]**。  
  
         **[挑選作業流程]** 對話方塊隨即開啟。 可用的排程會顯示為資料表。  
  
    3.  按一下含有所需排程的資料列。 例如，若要將排程變更為每 5 分鐘，請按一下排程名稱為 **CollectorSchedule_Every_5min**的資料列。  
  
        > [!NOTE]  
        >  您可以按一下 **[屬性]** 開啟排程的 **[作業排程屬性]** 對話方塊，藉以檢視和編輯選取之排程的屬性。 您可以使用這對話方塊來變更排程資訊，例如頻率。  
        >   
        >  除了修改現有的排程以外，您也可以按一下 **[上傳]** 頁面上的 **[新增]** 來建立新的上傳排程。 這個動作會開啟 **[新增作業排程]** 對話方塊，讓您可以用來建立自訂排程。  
  
    4.  當您完成排程的設定之後，請按一下 **[確定]**。  
  
         您所做的變更就會顯示在 **[上傳]** 頁面上。  
  
5.  按一下 **[確定]** 儲存對收集頻率和上傳排程所做的變更，並且關閉 **[資料收集組屬性]** 對話方塊。  
  
### <a name="to-change-the-schedule-for-a-non-cached-mode-collection-set"></a>若要變更非快取模式收集組的排程  
  
1.  在 [物件總管] 中，依序展開 **[管理]** 節點、 **[資料收集]**和 **[系統資料收集組]**。  
  
2.  以滑鼠右鍵按一下使用非快取模式的收集組 (例如 [磁碟使用量])，然後按一下 [屬性] 開啟 [[資料收集組屬性]](#CollectionSet) 對話方塊。  
  
     **[資料收集組屬性]** 對話方塊隨即顯示收集組屬性的分頁檢視。  
  
3.  若要變更收集組的排程，請按一下 **[挑選]**。  
  
     **[挑選作業流程]** 對話方塊隨即開啟。 可用的排程會顯示為資料表。  
  
4.  按一下含有所需排程的資料列。 例如，若要將排程變更為每 5 分鐘，請按一下排程名稱為 **CollectorSchedule_Every_5min**的資料列。  
  
    > [!NOTE]  
    >  您可以按一下 **[屬性]** 開啟排程的 **[作業排程屬性]** 對話方塊，藉以檢視和編輯選取之排程的屬性。 您可以使用這對話方塊來變更排程資訊，例如頻率。  
    >   
    >  除了修改現有的排程以外，您也可以按一下 **[一般]** 頁面上的 **[新增]** 來建立新的收集和上傳排程。 這個動作會開啟 **[新增作業排程]** 對話方塊。  
  
5.  當您完成排程的設定之後，請按一下 **[確定]**。  
  
6.  按一下 **[確定]** 儲存這些變更並且關閉 **[資料收集組屬性]** 對話方塊。  
  
####  <a name="CollectionSet"></a> 資料收集組屬性對話方塊  
 **一般頁面**  
  
 使用這個頁面可設定要如何收集及上傳資料、設定排程，以及設定管理資料倉儲中的資料保留期限。 這個頁面也會提供有關收集組的資訊，例如收集器類型和收集頻率，以及用於收集組的輸入參數。  
  
 **名稱**  
 顯示此頁面參考的收集組名稱。  
  
 **資料收集和上傳**  
 指定要如何收集資料並將其上傳到管理資料倉儲。 請挑選下列其中一個選項。  
  
|||  
|-|-|  
|**無快取 - 在相同排程時收集和上傳資料。**|當選取此選項時，請指定下列其中一項：<br /><br /> **排程**。 根據排程收集及上傳資料。 請按一下 **[挑選]** 從預先定義的排程清單中選取，或是按一下 **[新增]** 建立新的排程。<br /><br /> **視需要**。 視需要收集及上傳資料。|  
|**快取 - 以一組收集頻率來收集和快取資料，並在個別排程時上傳快取的資料。**|以指定的收集頻率來收集和快取資料。 根據個別排程上傳收集的資料。|  
  
 **收集項**  
 顯示收集組中的收集項。 下列資訊是針對每一個收集項所提供：  
  
-   **名稱**  
  
-   **收集器類型**  
  
-   **收集頻率** (秒)。 如果 **[資料收集和上傳]** 設定為 [快取]，就可以編輯這個欄位。 按兩下此資料格來設定收集頻率。  
  
 **輸入參數**  
 顯示用於收集組的輸入參數。  
  
 **執行身分**  
 指定用來執行收集組的帳戶。 根據預設，這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶。 如果定義了 Proxy 帳戶，這個清單就會包含可用 Proxy 帳戶的名稱。  
  
 **指定要將資料保留在管理資料倉儲中的天數。**  
 指定要將收集而來的資料保留多久。 請挑選下列其中一個選項。  
  
|||  
|-|-|  
|**資料保留期限**|預設會選取這個選項，而且預設的保留期限為 14 天。|  
|**永久保留資料**|對於資料的保留時間長度沒有任何時間限制。|  
  
 **上傳頁面**  
  
 使用這個頁面可針對此收集組所收集的資料來設定上傳排程。  
  
> [!NOTE]  
>  只有當已針對 [資料收集和上傳] 設定 [已快取] 選項時，才會啟用這個索引標籤。  
  
 **Server**  
 顯示將主控管理資料倉儲的伺服器名稱。 如需詳細資訊，請參閱[設定管理資料倉儲 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)。  
  
 **管理資料倉儲**  
 顯示管理資料倉儲的名稱。 如需詳細資訊，請參閱[設定管理資料倉儲 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)。  
  
 **上次上傳日期**  
 針對上次為此收集組完成的上傳顯示日期和時間資訊。  
  
 **上傳排程**  
 指定收集組的上傳排程。 當啟用這個選項時，請按一下 **[挑選]** 從預先定義的排程清單中選取，或是按一下 **[新增]** 建立新的排程。  
  
 **描述頁面**  
  
 使用此頁面可檢視此屬性頁面參考之收集組的描述。  
  
## <a name="see-also"></a>另請參閱  
 [管理資料收集](../../relational-databases/data-collection/manage-data-collection.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
