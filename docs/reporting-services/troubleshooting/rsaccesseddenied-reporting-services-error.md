---
title: "rsAccessedDenied-Reporting Services 錯誤 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7ece42006b7022bd3fa031cd95ef97767055ad53
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Reporting Services 錯誤
  當使用者沒有執行動作的權限時，會發生 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 錯誤 **rsAccessedDenied** 。 例如，他們並未擁有允許他們開啟報表的角色指派，或者他們沒有使用必要的權限開啟瀏覽器。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; SharePoint 模式|  
  
-   如果在直接透過 URL 存取報表伺服器時發生錯誤，則例外狀況會對應到 HTTP 401 錯誤。  
  
-   如果錯誤是在使用報表管理員或其他工具時發生，錯誤會顯示在錯誤頁面中。  
  
-   如果錯誤是在執行已排程的作業、訂閱或傳遞期間發生，則錯誤將只會顯示在報表伺服器記錄檔中。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|**產品名稱**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**事件識別碼**|rsAccessedDenied|  
|**事件來源**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**元件**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**訊息文字**|授與使用者 'mydomain\myAccount' 的權限不足，無法執行此作業。 (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>使用者動作  
 存取報表伺服器內容和作業的權限是透過角色指派而授與。 在新的安裝上，只有本機管理員具有存取報表伺服器的權限。 若要授與其他使用者存取權限，本機管理員必須建立角色指派，以指定網域使用者或群組帳戶、一個或多個角色 (用來定義使用者可執行的工作)，以及範圍 (通常是報表伺服器資料夾階層的 [主資料夾] 資料夾或根節點)。 您可以使用報表管理員來建立角色指派。 如需詳細資訊，請在《SQL Server 線上叢書》中搜尋「角色指派」。  
  
 這個錯誤是因為報表伺服器的本機管理所造成。 如需詳細資訊，請參閱[設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [角色指派](../../reporting-services/security/role-assignments.md)   
 [授與原生模式報表伺服器上的權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [角色和權限 &#40;Reporting Services &#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
  

