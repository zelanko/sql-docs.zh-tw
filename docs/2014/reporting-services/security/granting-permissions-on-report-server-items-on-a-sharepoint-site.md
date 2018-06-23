---
title: 授與 SharePoint 網站上報表伺服器項目的權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 5142c52b2a6a698e379957113d9540537282d80f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022808"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>授與 SharePoint 網站上報表伺服器項目的權限
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 提供內建的安全性功能，可用來授與從 SharePoint 網站和文件庫存取報表伺服器項目的權限。 如果您已經指定權限給使用者，則在設定 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 與報表伺服器之間的整合設定之後，那些使用者就能立即存取報表伺服器項目和作業。 您可以使用現有權限來上傳報表定義和其他文件、檢視報表、建立訂閱和管理項目。  
  
 如果您未指定權限，或是不熟悉 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]中的安全性功能，請依照下列方針進行：  
  
1.  在 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]的產品文件中，閱讀有關標準 SharePoint 群組的預設安全性設定，以了解如何管理權限和使用者存取。  
  
2.  檢閱會明確影響報表伺服器項目和作業存取權的權限清單。 如需詳細資訊，請參閱[報表伺服器項目的 Windows SharePoint Services 中使用內建安全性](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。  
  
3.  指定使用者和群組帳戶給預先定義的 SharePoint 群組。  
  
4.  或者，建立新的權限等級和群組，或修改現有的權限等級和群組，以便隨特定需要改變伺服器存取權限。  
  
 若要搭配報表伺服器項目使用 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 安全性功能，您必須擁有以 SharePoint 整合模式執行的報表伺服器。  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>關於權限、權限等級和 SharePoint 群組  
 下列清單提供 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]中安全性功能的簡介。 如需詳細資訊，請參閱 SharePoint 網站上的「Windows SharePoint 說明與使用方法」。  
  
-   安全物件包括網站、清單、文件庫、資料夾和文件。  
  
-   權限是可執行特定工作的授權。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 提供 33 種預先定義的權限，可合併成為權限等級。  
  
-   權限等級是可授與使用者或 SharePoint 群組的安全性實體物件 (例如網站、文件庫、清單、資料夾、項目或文件) 權限集合。 它相當於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的角色定義。 預先定義的權限等級有 5 個。 您可以進行自訂或視需要建立新的。  
  
-   SharePoint 群組是您可以在 SharePoint 網站上建立的使用者群組，以管理站台的權限或提供站台成員的電子郵件通訊群組清單。 SharePoint 群組包含 Windows 使用者和群組帳戶，或使用者登入 (如果您是使用表單驗證)。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 提供三個群組。 您可以進行自訂或視需要建立新的。  
  
-   權限繼承讓子網站、清單、文件庫和項目能夠繼承上層網站的安全性設定。 您可以使用繼承的權限來存取儲存在 SharePoint 文件庫中的報表伺服器項目。 使用權限繼承和預先定義的 SharePoint 群組有助於簡化您的部署，並可立即存取大部分報表伺服器作業。  
  
## <a name="who-sets-permissions"></a>誰設定權限  
 安裝 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、執行 SharePoint 組態精靈並建立入口網站的管理員會成為預設的入口網站擁有者。 網站擁有者可以在管理中心中設定伺服陣列或獨立 SharePoint Web 應用程式的權限，也可以設定每個 SharePoint Web 應用程式於頂層網站的權限。 這個人也可以指定其他網站擁有者。  
  
 在 SharePoint Web 應用程式的頂層網站，網站集合管理員可設定整個網站階層中多個網站的權限。 個別網站擁有者可以執行與子網站相關的相同工作。  
  
 伺服器管理員和網站集合管理員可以設定選項，以決定其他網站擁有者能否設定權限。 依您擁有的不同權限等級，您或許無法建立或自訂 SharePoint 群組或權限等級。  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>使用預先定義的 SharePoint 群組和權限等級  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 產品文件中的建議事項建議您使用標準 SharePoint 群組 (它們是「 *Site name* **擁有者**, *Site name* **成員**」和「 *Site name* **訪客**」)，並於網站層級指定權限。 受您指定權限的大部分使用者應該是「 *Site name* **訪客** 」或「 *Site name* **成員** 」群組的成員。 上層網站的權限會由整個網站階層繼承。 您可以針對需要其他限制的特定項目，中斷其權限繼承。  
  
 下列 SharePoint 群組具有下列預先定義的權限等級：  
  
-   「 **擁有者** 」群組具有「完整控制權」權限，讓群組成員能夠變更網站內容、網頁或功能。 完整控制存取權應該僅限於網站管理員。  
  
-   「 **成員** 」群組具有「參與」等級權限，讓群組成員能夠檢視網頁、編輯項目、提交變更核准、加入清單項目和刪除清單項目。  
  
-   [訪客]  群組具有「讀取」層級權限，讓群組成員能夠檢視網頁、清單項目和文件。  
  
 SharePoint 群組具有可立即存取許多報表伺服器作業的權限等級。 如果您覺得內建的安全性設定無法提供您需要的存取層級，您可以建立自訂群組或權限等級。  
  
 如需哪一個報表伺服器作業支援的透過預設的安全性功能的詳細資訊，請參閱[報表伺服器項目的 Windows SharePoint Services 中使用內建安全性](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。  
  
 若要使用內建的安全性功能，您必須將 Windows 使用者或群組帳戶指定給 SharePoint 群組。 但伺服器管理員和入口網站擁有者除外，因為在安裝軟體時，他們就自動具有 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 的存取權，至於所有其他使用者都必須經過授與權限後，才能存取伺服器。  
  
## <a name="in-this-section"></a>本節內容  
 [在 Windows SharePoint Services 中使用報表伺服器項目的內建安全性](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 說明如何使用預先定義的 SharePoint 群組和權限等級來存取報表伺服器項目。  
  
 [報表伺服器項目的 SharePoint 網站和清單權限參考](sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 提供可用來存取報表伺服器作業之所有 SharePoint 產品權限的參考。  
  
 [設定 SharePoint Web 應用程式中報表伺服器作業的權限](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 描述隨選報表的權限需求，並建議啟用功能的方法。  
  
 [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 提供簡短摘要，將 SharePoint 群組與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中預先定義的角色定義做比較。  
  
 [在 SharePoint 網站上設定報表伺服器項目的權限&#40;的 Reporting Services SharePoint 整合模式&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 提供指示，以建立有權可啟動報表產生器和設定模型項目安全性的新 SharePoint 群組。 本主題也包含有關為任何報表伺服器項目或作業設定自訂權限的一般指導方針。  
  
## <a name="see-also"></a>另請參閱  
 [在 SharePoint 網站上設定報表伺服器項目的權限&#40;的 Reporting Services SharePoint 整合模式&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services 安全性與保護](reporting-services-security-and-protection.md)  
  
  