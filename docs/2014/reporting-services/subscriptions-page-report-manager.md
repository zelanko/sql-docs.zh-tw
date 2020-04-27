---
title: 訂閱頁面（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: cf3a6bd0-e0b2-4875-a532-63ef34cfa860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec92d7c58b68b14374666f65489f145fa863422
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101093"
---
# <a name="subscriptions-page-report-manager"></a>訂閱頁面 (報表管理員)
  使用 [訂閱] 頁面即可列出目前報表或共用資料來源的全部訂閱。 如果您擁有足夠的權限 (如同「管理所有訂閱」工作所表示)，就可以檢視所有使用者的訂閱。 否則，此頁面只會顯示您擁有的訂閱。  
  
> [!NOTE]  
>  其他頁面也會包含訂閱資訊。 如需詳細資訊，請參閱[我的訂閱頁面 &#40;報表管理員&#41;](../../2014/reporting-services/my-subscriptions-page-report-manager.md)在同一個位置存取您所有的訂用帳戶，或使用 [[新增訂閱] 或 [編輯訂閱] 頁面 &#40;報表管理員](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md)&#41;建立或編輯訂用帳戶。  
  
 有些選項只會在有現有的訂閱可用時才看得見。 如果未定義任何訂閱，而且您是從報表中存取此頁面，頁面上就只會有 **[新增訂閱]** 和 **[新增資料驅動訂閱]** 選項。  
  
 建立新訂閱之前，您必須確認報表資料來源是否使用預存認證。 使用 [資料來源屬性] 頁面即可儲存認證。 如需詳細資訊，請參閱[資料來源屬性頁面 &#40;報表管理員&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需版本支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱[SQL Server 2014 版本支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-subscriptions-page-for-report"></a>若要開啟報表的訂閱頁面  
  
1.  開啟報表管理員，然後找出您想要檢視或設定訂閱的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該報表的 [一般] 屬性頁面。  
  
4.  選取 **[訂閱]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **刪除**  
 按一下即可刪除訂閱。 在刪除訂閱之前，請選取您想要刪除之每一個訂閱旁邊的核取方塊。  
  
 **新增訂用帳戶**  
 按一下即可建立目前報表的新訂閱。 當報表使用預存認證或無認證時，就會啟用此按鈕。 當您開啟共用資料來源的 [訂閱] 頁面時，無法使用此按鈕。  
  
 **[新增資料驅動訂閱]**  
 按一下即可針對包含此資訊之資料存放區執行的命令或查詢，產生訂閱者清單和傳遞選項。 當報表使用預存認證或無認證時，就會啟用此按鈕。 當您開啟共用資料來源的 [訂閱] 頁面時，無法使用此按鈕。  
  
 **編輯**  
 按一下即可檢視或編輯訂閱。  
  
 **Report**  
 當您從共用資料來源開啟這個頁面時，此資料行會識別定義此訂閱的報表。 **[資料夾]** 資料行會識別報表的位置。  
  
 **描述**  
 顯示訂閱的描述。  
  
 **觸發程序**  
 識別造成執行訂閱的條件。 **TimedSubscription** 觸發程序是以執行訂閱時定義的排程為基礎。 **SnapshotUpdated** 觸發程序是以報表快照集的更新為基礎。  
  
 **擁有者**  
 顯示建立訂閱的使用者名稱。  
  
 **最後執行**  
 顯示最後處理訂閱的時間。  
  
 **狀態**  
 顯示訂閱的狀態。 通常，狀態值若不是新的 (New)，就會是上一次執行訂閱的日期和時間。  
  
 訂閱若是包含指向 (對執行報表所使用的預存認證) 已經無效之加密值的指標，則會出現「不正確的資料」狀態值。 在報表伺服器上重新建立用於加密和解密資料的對稱金鑰時，現有的加密值將變成無法使用。  
  
 如果訂閱已經停用，則無法處理該訂閱。 若要更新訂閱並讓其運作，請開啟然後儲存訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [以原生模式 &#40;Reporting Services 建立、修改和刪除標準訂閱&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [建立、修改和刪除共用排程](subscriptions/create-modify-and-delete-schedules.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
