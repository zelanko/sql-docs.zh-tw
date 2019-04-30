---
title: 新的訂用帳戶或編輯訂閱頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e02d6529-ce67-4305-b7f0-433997e99c21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 926223ad0a5a8cdb1a5ff7aacfb7fdd7f84a8c57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188324"
---
# <a name="new-subscription-or-edit-subscription-page-report-manager"></a>新增訂閱或編輯訂閱頁面 (報表管理員)
  使用 [新增訂閱] 或 [編輯訂閱] 頁面，即可在報表中建立新的訂閱或修改現有的訂閱。 這個頁面的此選項隨著您的角色指派而改變。 具有進階權限的使用者可以使用額外的選項。  
  
 可自主式執行的報表支援訂閱。 報表至少必須使用預存認證或無認證。 如果報表使用參數，就必須指定預設值。 如果您變更報表執行設定或移除參數屬性的預設值，就可能會造成訂閱停用。 如需詳細資訊，請參閱 [建立和管理原生模式報表伺服器的訂閱](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-new-subscription-or-edit-subscription-page"></a>若要開啟新增訂閱或編輯訂閱頁面  
  
1.  開啟報表管理員，然後找出您想要加入訂閱的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，執行下列其中一項步驟：  
  
    -   按一下 **[管理]**。 這樣就會開啟該報表的 [一般] 屬性頁面。 然後，選取 **[訂閱]** 索引標籤。在工具列中，按一下 **[新增訂閱]**，或選取現有訂閱，然後按一下 **[編輯]**。  
  
    -   按一下 **[訂閱]**。 這樣就會開啟該報表的 **[新增訂閱]** 頁面。  
  
## <a name="options"></a>選項。  
 **傳遞者**  
 選取要用來散發報表的傳遞延伸模組。 系統會根據您所選取的傳遞延伸模組顯示下列設定：  
  
-   電子郵件訂閱提供電子郵件使用者很熟悉的欄位 (例如， **[收件者]**、 **[主旨]**，以及 **[優先權]** 等欄位)。 指定 **[包含報表]** 即可內嵌或附加報表，或是指定 **[包含連結]** 以包含連結到報表的 URL。 指定 **[轉譯格式]** 即可為附加或內嵌的報表選擇呈現格式。  
  
-   檔案共用訂閱提供讓您指定目標位置的欄位。 您可以傳遞任何報表至檔案共用。 不過，支援互動式功能的報表 (包括支援針對資料列和資料行向下鑽研的矩陣報表) 將轉譯成靜態檔案。 您無法在靜態檔案中檢視向下鑽研資料列和資料行。 檔案共用名稱必須以統一命名慣例 (UNC) 格式指定 (例如\\\mycomputer\public\myreportfiles)。 在路徑名稱中不可包含反斜線。 報表檔案會使用以轉譯格式為基礎的檔案格式進行傳遞 (例如，如果您選擇了 **[Excel]**，報表就會以 .xls 檔案來傳遞)。  
  
 傳遞延伸模組是否可用，取決於該模組是否安裝和設定於報表伺服器。 報表伺服器電子郵件是預設傳遞延伸模組，但您必須先設定它才能夠使用。 檔案共用傳遞不需要進行設定，但您必須先定義共用資料夾，才能加以使用。  
  
## <a name="subscription-processing-options"></a>訂閱處理選項  
 使用這些設定來定義使訂閱開始處理的狀況。 有些選項只能在使用參數的報表或以報表執行快照集執行的報表中使用。  
  
 **重新整理報表內容時**  
 選擇此選項以訂閱依排程重新整理的報表快照集。 只有在訂閱以報表執行快照集執行的報表時，才看得見這個選項。 報表執行快照集的內容通常會定期重新整理。 對於以此模式執行的報表，您可以將訂閱定義為重新整理快照集時發生。  
  
 **當排程的報表執行完成時**  
 建立決定何時處理訂閱的排程。  
  
 **在共用排程上**  
 選擇預先定義的排程以處理訂閱。  
  
 **輸入參數值**  
 當您訂閱具有參數的報表時，請使用此選項。 此選項只能用於參數化的報表。 訂閱參數化報表時，可以指定用來建立透過訂閱傳遞之報表版本所使用的參數值。 例如，您可以指定區域碼，以選取特定區域的業務資料。 若未指定任何值，就會使用預設值。  
  
## <a name="see-also"></a>另請參閱  
 [為電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [建立、修改和刪除共用排程](subscriptions/create-modify-and-delete-schedules.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
