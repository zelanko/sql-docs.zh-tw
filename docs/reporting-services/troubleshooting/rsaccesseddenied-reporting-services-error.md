---
title: rsAccessedDenied - Reporting Services 錯誤 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0063256e371585fe6d63a1a635aa286fca5a7d39
ms.sourcegitcommit: 9388dcccd6b89826dde47b4c05db71274cfb439a
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270230"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Reporting Services 錯誤
  當使用者沒有執行動作的權限時，會發生 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 錯誤 **rsAccessedDenied** 。 例如，他們並未擁有允許他們開啟報表的角色指派，或是沒有使用必要的權限來開啟瀏覽器。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; SharePoint 模式|  
  
- 如果在直接透過 URL 存取報表伺服器時發生錯誤，則例外狀況會對應到 HTTP 401 錯誤。  
  
- 如果該錯誤是在使用入口網站時發生，該例外狀況通常會對應至 HTTP 401 錯誤，或是其他已定義的 HTML 錯誤頁面。  
  
- 如果錯誤是在執行已排程的作業、訂閱或傳遞期間發生，則錯誤將只會顯示在報表伺服器記錄檔中。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|**產品名稱**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**事件識別碼**|rsAccessedDenied|  
|**事件來源**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**元件**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**訊息文字**|授與使用者 'mydomain\myAccount' 的權限不足，無法執行此作業。 (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>使用者動作  
 存取報表伺服器內容和作業的權限是透過角色指派而授與。 在新的安裝上，只有本機管理員具有存取報表伺服器的權限。 若要授與其他使用者存取權限，本機管理員必須建立角色指派，以指定網域使用者或群組帳戶、一個或多個角色 (用來定義使用者可執行的工作)，以及範圍 (通常是報表伺服器資料夾階層的 [主資料夾] 資料夾或根節點)。 您可以使用入口網站來建立角色指派。 如需相關資訊，請參閱[角色指派](../../reporting-services/security/role-assignments.md)。  
  
 這個錯誤是因為報表伺服器的本機管理所造成。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [角色指派](../../reporting-services/security/role-assignments.md)  
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 [角色與權限 &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  