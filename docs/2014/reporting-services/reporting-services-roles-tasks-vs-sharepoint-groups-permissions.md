---
title: 將 Reporting Services 中的角色和工作與 SharePoint 群組和許可權做比較 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1c56b15a5d6887c3e00047c9a0c3a66f907ef468
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102805"
---
# <a name="compare-roles-and-tasks-in-reporting-services-to-sharepoint-groups-and-permissions"></a>將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較
  本主題會比較 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式中的角色和工作型授權功能與 SharePoint 產品的安全性功能。 本主題會比較有關角色、工作、SharePoint 群組、權限等級和權限的詞彙與特性。  
  
||  
|-|  
|[!INCLUDE[applies](../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Sharepoint 模式 &#124; sharepoint 2010 和 SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]原生模式|  
  
 **本主題內容：**  
  
-   [比較許可權工具和詞彙](#bkmk_compare_tools_terms)  
  
-   [比較原生模式角色和 SharePoint 群組](#bkmk_compare_roles_groups)  
  
-   [比較原生模式工作和 SharePoint 許可權](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a>比較許可權工具和詞彙  
 **原生模式：**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]原生模式權限物件（角色和工作）是在中[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]建立，並針對報表管理員中的個別使用者進行設定。  
  
 **Sharepoint 模式：** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sharepoint 模式會利用 sharepoint 許可權功能。 SharePoint 群組和權限是從 **[站台設定]** 頁面管理。  
  
 下表比較 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式和 SharePoint 之間的權限相關物件及概念。  
  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]原生模式|SharePoint|  
|---------------------------------------------|----------------|  
|**角色：** 例如「內容管理員」。|**群組：** 例如，預設的「檢視器」群組。|  
|---|**許可權等級群組：** 例如「僅限 View」代表「檢視器」群組。|  
|工作 **：** 例如 [管理報表]。|**許可權：** 例如，在「僅 View」群組中，有 [視圖專案]、[view 版本] 和 [view] 應用程式頁面的清單相關許可權。|  
  
 如需 SharePoint 許可權的詳細資訊，請參閱[Sharepoint Server 中的使用者權限與許可權等級](/sharepoint/sites/user-permissions-and-permission-levels)，並[決定 sharepoint 2013 中的許可權等級和群組](https://technet.microsoft.com/library/cc262690.aspx)。  
  
##  <a name="bkmk_compare_roles_groups"></a>比較原生模式角色和 SharePoint 群組  
 下表會比較 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式中的預先定義角色定義與標準 SharePoint 群組。 如果 SharePoint 群組不符合您所需要的特定角色，您可以在 SharePoint 中建立自訂群組，並指派權限等級。  
  
 **注意**：可用的預設 sharepoint 群組取決於用來建立 SharePoint 網站的網站範本。  
  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]角色|SharePoint 群組|  
|--------------------------------------|-----------------------|  
|**[瀏覽器]**<br /><br /> 檢視|
  **
  ** 使用 [訪客] 群組可授與檢視報表的權限。 
  **
  ** [訪客] 群組具有「讀取」層級權限，讓群組成員能夠檢視網頁、清單項目和文件。|  
|**內容管理員**<br /><br /> 對所有項目和項目層級的作業具有完整權限，其中包括設定安全性的權限。|使用「 **擁有者** 」群組可授與完整控制權，來管理 SharePoint 網站上的報表伺服器項目。 「 **擁有者** 」群組具有「完整控制權」權限，讓群組成員能夠變更網站內容、網頁或功能。 完整控制存取權應該僅限於網站管理員。|  
|**我的報表**|沒有對等的群組。 以 SharePoint 模式執行的報表伺服器不支援**我的報表**。 如果您想要使用對等的功能，可以使用 [!INCLUDE[winSPServ](../includes/winspserv-md.md)] 中的「我的網站」功能。|  
|**發行者**<br /><br /> 加入、更新、檢視和刪除報表、報表模型、共用資料來源和資源。|使用「 **成員** 」群組可授與權限，在 SharePoint 網站上加入項目、編輯項目和更新相依項目的參考。 「 **成員** 」群組具有「參與」等級權限，讓群組成員能夠檢視網頁、加入和更新項目以及提交變更核准。|  
|**報表產生器**<br /><br /> 在報表產生器中檢視報表、自我管理個別訂閱和開啟報表。|在預先定義的現成權限等級或 SharePoint 群組中，沒有相當於報表產生器報表定義的項目。 依預設，凡是屬於「 **成員** 」群組或「 **擁有者** 」群組的使用者，都有權限可以使用報表產生器。 如果您要讓更多使用者可以使用報表產生器，您應該建立自訂安全性設定，以提供類似報表產生器角色所提供的權限等級。 如需詳細資訊，請參閱 [設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)＞。|  
|-|
  **
  ** 使用 [檢視者] 群組可授與檢視已轉譯之報表的權限。 「 **檢視者** 」群組無法下載或檢視報表項目的內容。<br /><br /> **注意：** 從 SQL Server 2012 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]開始，**查看**器群組沒有建立訂閱的許可權。|  
|**系統使用者**和**系統管理員**|這些角色不是以 SharePoint 模式執行報表伺服器時必要的角色。 **系統使用者**和**系統管理員**會對應到 SharePoint 伺服器陣列或 Web 應用層級許可權。 報表伺服器不提供必須於該層級授權的任何功能。|  
  
##  <a name="bkmk_compare_tasks_permissions"></a>比較原生模式工作和 SharePoint 許可權  
 下表會比較 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式工作與 SharePoint 權限。 
  **[類型]** 資料行指出原生模式工作是否與系統角色或標準角色和項目相關。 系統角色管理系統層級的權限，例如共用排程。  
  
|原生模式工作|角色類型|對等的 SharePoint 權限|  
|----------------------|---------------|--------------------------------------|  
|取用報表|Item|編輯項目、檢視項目。|  
|建立連結報表|Item|不支援。|  
|管理所有訂閱|Item|管理「警示」。|  
|管理資料來源|Item|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理資料夾|Item|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理個別訂閱|Item|編輯項目<br /><br /> 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]之前，必要權限層級是建立警示。|  
|管理模型|Item|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理報表記錄|Item|編輯項目、檢視版本、刪除版本。|  
|管理報表|Item|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理資源|Item|加入項目、編輯項目、刪除項目、檢視項目。|  
|設定個別項目的安全性|Item|管理權限|  
|檢視資料來源|Item|檢視項目。|  
|檢視資料夾|Item|檢視項目。|  
|檢視模型|Item|檢視項目。|  
|檢視報表|Item|檢視項目。|  
|檢視資源|Item|檢視項目。|  
||||  
|執行報表定義|系統|檢視項目。|  
|產生事件|系統|管理網站。|  
|管理工作|系統|無 (不支援)。|  
|管理報表伺服器屬性|系統|無 (不適用)。 報表伺服器不控制使用者在管理中心是否有權限檢視整合設定。|  
|管理角色|系統|管理權限。|  
|管理共用排程|系統|管理網站、開啟。|  
|管理報表伺服器安全性|系統|無 (不適用)。 在以 SharePoint 整合模式執行的伺服器上，報表伺服器不使用系統層級角色指派。|  
|檢視報表伺服器屬性|系統|無 (不適用)。 報表伺服器不控制使用者在管理中心是否有權限檢視整合設定。|  
|檢視共用排程|系統|開啟項目。|  
  
## <a name="see-also"></a>另請參閱  
 [在 sharepoint 網站上設定報表伺服器專案的許可權 &#40;SharePoint 整合模式中的 Reporting Services&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [設定 SharePoint Web 應用程式中報表伺服器作業的權限](security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [角色定義](security/role-definitions.md)   
 [預先定義的角色](security/role-definitions-predefined-roles.md)  
  
  
