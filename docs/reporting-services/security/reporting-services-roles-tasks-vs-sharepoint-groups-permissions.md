---
title: Reporting Services 角色工作與SharePoint 群組權限 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dfbab3b4af007cfd7694e45176131cb6c931b3fb
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210157"
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Reporting Services 角色工作與SharePoint 群組權限
  本主題會比較 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式中的角色和工作型授權功能與 SharePoint 產品的安全性功能。 本主題會比較有關角色、工作、SharePoint 群組、權限等級和權限的詞彙與特性。  
  
||  
|-|  
| [!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 &#124; SharePoint 2010 和 SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
 **本主題內容：**  
  
-   [比較權限工具和詞彙](#bkmk_compare_tools_terms)  
  
-   [比較原生模式角色和 SharePoint 群組](#bkmk_compare_roles_groups)  
  
-   [比較原生模式工作和 SharePoint 權限](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> 比較權限工具和詞彙  
 **原生模式：**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式權限物件 (角色和工作) 是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立，並為報表管理員的個別使用者設定。  
  
 **SharePoint 模式：**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式會利用 SharePoint 權限功能。 SharePoint 群組和權限是從 **[站台設定]** 頁面管理。  
  
 下表比較 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式和 SharePoint 之間的權限相關物件及概念。  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|SharePoint|  
|---------------------------------------------|----------------|  
|**角色：** 例如 [內容管理員]。|**群組：** 例如預設 [檢視者] 群組。|  
|---|**權限等級群組：** 例如 [檢視者] 群組的 [僅檢視]。|  
|**工作：** 例如「管理報表」。|**權限：** 例如，在 [僅檢視] 群組中有檢視項目、檢視版本和檢視應用程式頁面的清單相關權限。|  
  
 如需有關 SharePoint 權限的詳細資訊，請參閱＜ [權限等級和權限](https://office.microsoft.com/windows-sharepoint-services-help/permission-levels-and-permissions-HA010100149.aspx) ＞和＜ [在 SharePoint 2013 中決定權限層級及群組](https://technet.microsoft.com/library/cc262690.aspx)＞。  
  
##  <a name="bkmk_compare_roles_groups"></a> 比較原生模式角色和 SharePoint 群組  
 下表會比較 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式中的預先定義角色定義與標準 SharePoint 群組。 如果 SharePoint 群組不符合您所需要的特定角色，您可以在 SharePoint 中建立自訂群組，並指派權限等級。  
  
 **注意**:可用的預設 SharePoint 群組取決於用來建立 SharePoint 網站的網站範本。  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 角色|SharePoint 群組|  
|--------------------------------------|-----------------------|  
|**瀏覽器**<br /><br /> 檢視| 使用 [訪客] 群組可授與檢視報表的權限。  [訪客] 群組具有「讀取」層級權限，讓群組成員能夠檢視網頁、清單項目和文件。|  
|**內容管理員**<br /><br /> 對所有項目和項目層級的作業具有完整權限，其中包括設定安全性的權限。|使用「 **擁有者** 」群組可授與完整控制權，來管理 SharePoint 網站上的報表伺服器項目。 「 **擁有者** 」群組具有「完整控制權」權限，讓群組成員能夠變更網站內容、網頁或功能。 完整控制存取權應該僅限於網站管理員。|  
|**我的報表**|沒有對等的群組。  以 SharePoint 模式執行的報表伺服器不支援 [我的報表]。 如果您想要使用對等的功能，可以使用 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 中的「我的網站」功能。|  
|**發行者**<br /><br /> 加入、更新、檢視和刪除報表、報表模型、共用資料來源和資源。|使用「 **成員** 」群組可授與權限，在 SharePoint 網站上加入項目、編輯項目和更新相依項目的參考。 「 **成員** 」群組具有「參與」等級權限，讓群組成員能夠檢視網頁、加入和更新項目以及提交變更核准。|  
|**報表產生器**<br /><br /> 在報表產生器中檢視報表、自我管理個別訂閱和開啟報表。|在預先定義的現成權限等級或 SharePoint 群組中，沒有相當於報表產生器報表定義的項目。 依預設，凡是屬於「 **成員** 」群組或「 **擁有者** 」群組的使用者，都有權限可以使用報表產生器。 如果您要讓更多使用者可以使用報表產生器，您應該建立自訂安全性設定，以提供類似報表產生器角色所提供的權限等級。 如需詳細資訊，請參閱 [設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)＞。|  
|-| 使用 [檢視者] 群組可授與檢視已轉譯之報表的權限。 「 **檢視者** 」群組無法下載或檢視報表項目的內容。<br /><br /> **注意：** 從 SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 開始，[檢視者] 群組沒有建立訂閱的權限。|  
|**系統使用者** 和 **系統管理員**|這些角色不是以 SharePoint 模式執行報表伺服器時必要的角色。  [系統使用者]  和 [系統管理員] 對應到 SharePoint 伺服陣列或 Web 應用程式層級權限。 報表伺服器不提供必須於該層級授權的任何功能。|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> 比較原生模式工作和 SharePoint 權限  
 下表會比較 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式工作與 SharePoint 權限。 **[類型]** 資料行指出原生模式工作是否與系統角色或標準角色和項目相關。 系統角色管理系統層級的權限，例如共用排程。  
  
|原生模式工作|角色類型|對等的 SharePoint 權限|  
|----------------------|---------------|--------------------------------------|  
|取用報表|項目|編輯項目、檢視項目。|  
|建立連結報表|項目|不支援。|  
|管理所有訂閱|項目|管理警示。|  
|管理資料來源|項目|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理資料夾|項目|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理個別訂閱|項目|編輯項目<br /><br /> 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之前，必要權限層級是建立警示。|  
|管理模型|項目|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理報表記錄|項目|編輯項目、檢視版本、刪除版本。|  
|管理報表|項目|加入項目、編輯項目、刪除項目、檢視項目。|  
|管理資源|項目|加入項目、編輯項目、刪除項目、檢視項目。|  
|設定個別項目的安全性|項目|管理權限|  
|檢視資料來源|項目|檢視項目。|  
|檢視資料夾|項目|檢視項目。|  
|檢視模型|項目|檢視項目。|  
|檢視報表|項目|檢視項目。|  
|檢視資源|項目|檢視項目。|  
||||  
|執行報表定義|系統|檢視項目。|  
|產生事件|系統|管理網站。|  
|管理作業|系統|無 (不支援)。|  
|管理報表伺服器屬性|系統|無 (不適用)。 報表伺服器不控制使用者在管理中心是否有權限檢視整合設定。|  
|管理角色|系統|管理權限。|  
|管理共用排程|系統|管理網站、開啟。|  
|管理報表伺服器安全性|系統|無 (不適用)。 在以 SharePoint 整合模式執行的伺服器上，報表伺服器不使用系統層級角色指派。|  
|檢視報表伺服器屬性|系統|無 (不適用)。 報表伺服器不控制使用者在管理中心是否有權限檢視整合設定。|  
|檢視共用排程|系統|開啟項目。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [設定 SharePoint Web 應用程式中報表伺服器作業的權限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [角色定義](../../reporting-services/security/role-definitions.md)   
 [預先定義的角色](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
