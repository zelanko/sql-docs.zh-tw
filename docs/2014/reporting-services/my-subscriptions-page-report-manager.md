---
title: 我的訂閱頁面（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 491a85a3-f323-4155-a0a8-de2779899995
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 75d662f677ee2b6bbab8e445804ca7f142b5c034
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108193"
---
# <a name="my-subscriptions-page-report-manager"></a>我的訂閱頁面 (報表管理員)
  使用 [我的訂閱] 頁面來檢視某個位置的所有訂閱。 從這個頁面中，您可以存取與修改或刪除擁有的任何訂閱。 您只擁有您所建立的訂閱。 您不可以存取其他使用者的訂閱，也不可以存取您有權使用但並未擁有的訂閱 (例如，如果您的名稱已經加入另一位使用者所定義的現有訂閱中)。 您不可以在此頁面建立訂閱。 如需有關建立訂閱的詳細資訊，請參閱 [[新增訂閱] 或 [編輯訂閱] 頁面 &#40;報表管理員&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md)。  
  
 在預設狀況下，依報表名稱的字母順序來排序訂閱。 按一下不同的資料行標題，變更訂閱的排序方式。 如果您沒有訂閱或者建立或管理訂閱的權限已停用，頁面上將不會出現任何訂閱。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需版本支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱[SQL Server 2014 版本支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-my-subscriptions-page"></a>若要開啟我的訂閱頁面  
  
1.  開啟報表管理員。  
  
2.  在頁面的頂端，按一下右邊角落的 [我的訂閱]。  
  
    > [!NOTE]  
    >  [我的訂閱] 永遠可以使用，即使您沒有建立訂閱的權限。  
  
## <a name="options"></a>選項。  
 **刪除**  
 選取您要刪除的每一個訂閱旁邊的核取方塊，然後按一下 **[刪除]**。  
  
 **編輯**  
 按一下即可檢視或編輯訂閱。  
  
 **Report**  
 顯示在訂閱中指定的報表。 按一下報表名稱即可檢視報表。  
  
 **描述**  
 顯示訂閱的描述。 按一下描述即可檢視或編輯報表的訂閱資訊。  
  
 **資料夾**  
 顯示包含訂閱中指定之報表的資料夾。 按一下資料夾名稱即可檢視資料夾的內容。  
  
 **觸發程序**  
 識別造成執行訂閱的條件。 **TimedSubscription** 觸發程序是以執行訂閱時定義的排程為基礎。 **SnapshotUpdated** 觸發程序是以報表快照集的更新為基礎。  
  
 **最後執行**  
 顯示最後處理訂閱的時間。  
  
 **狀態**  
 顯示訂閱的狀態。 通常狀態值為「新增」，或上次執行訂閱的日期和時間。  
  
 訂閱若是包含指向 (對執行報表所使用的預存認證) 已經無效之加密值的指標，則會出現「不正確的資料」狀態值。 在報表伺服器上重新建立用於加密和解密資料的對稱金鑰時，現有的加密值將變成無法使用。  
  
 如果訂閱已經停用，則無法處理該訂閱。 若要更新訂閱並讓其運作，請開啟然後儲存訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
