---
title: "Power Pivot for SharePoint 2016 的最低權限組態範例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 35757f68-7bfc-4906-a985-f369690b9237
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Power Pivot for SharePoint 2016 的最低權限組態範例
  本主題描述使用最低權限的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2016 組態範例。 此組態會分別針對三個元件使用不同的帳戶，而且每個帳戶都具有最低層級的權限。  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
## 帳戶摘要  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2016 支援使用網路服務帳戶作為 Analysis Services 服務帳戶。 網路服務帳戶並非 SharePoint 2010 的支援案例。 如需服務帳戶的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](http://msdn.microsoft.com/library/ms143504.aspx) (http://msdn.microsoft.com/library/ms143504.aspx)。  
  
 下表將摘要說明用於這個最低權限組態範例的三個帳戶。  
  
|範圍。|名稱|  
|-----------|----------|  
|SharePoint 管理員帳戶|**SPAdmin**|  
|SharePoint 伺服器陣列帳戶|**SPFarm**|  
|Analysis Services 服務帳戶|**SPsvc**|  
  
### SharePoint 管理員帳戶 (SpAdmin)  
 **SPAdmin** 是您用來安裝和設定伺服器陣列的網域帳戶。 這個帳戶用來執行 [SharePoint 組態精靈] 以及適用於 SharePoint 2016 的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具。**SPAdmin** 帳戶是唯一需要本機系統管理員權限的帳戶。 執行 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具之前，請將 **SPAdmin** 帳戶權限授與 SQL Server 資料庫執行個體，其為 SharePoint 建立內容和組態資料庫的位置。 若要在最低權限案例中設定 SPAdmin 帳戶，它必須是 **securityadmin** 和 **dbcreator** 角色的成員。  
  
### 伺服器陣列帳戶 (SPFarm)  
 **SPFarm** 是 SharePoint Timer Service 和管理中心 Web 應用程式用來存取 SharePoint 內容資料庫的網域帳戶。 這個帳戶不需要是本機系統管理員。 [SharePoint 組態精靈] 會授與後端 SQL Server 資料庫的適當最低權限。最低 SQL Server 權限組態就是 **securityadmin** 和 **dbcreator** 角色的成員資格。  
  
### Power Pivot 服務的服務帳戶 (SPsvc)  
 如果您沒有在執行 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具之前設定新的 SharePoint 伺服器陣列，則 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具預設將建立下列項目：  
  
-   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式。  
  
-   安全存放應用程式。  
  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具會在預設應用程式集區中設定這兩個服務應用程式。 該應用程式集區通常設定為以 SPFarm 帳戶的身分執行，這個帳戶可存取服務帳戶不需要的許多資源。 若要讓環境成為最低權限的環境，請設定要由適當應用程式集區和 Web 應用程式使用的新網域帳戶。  
  
 **若要建立要當做 SharePoint 服務帳戶使用的新網域帳戶 SPsvc：**  
  
1.  在 SharePoint 管理中心，選取 [安全性]。  
  
2.  選取 [設定服務帳戶]  
  
3.  選取 [註冊新的受管理帳戶]。  
  
 **SPSvc** 帳戶沒有任何本機系統管理員權限，而且 SPsvc 沒有 SharePoint 資料庫的任何權限。 SPsvc 所需的唯一權限就是 Analysis Services 之 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 執行個體的系統管理權限。  
  
 **若要將適當的應用程式集區設定為使用 SPsvc 帳戶：**  
  
1.  在 SharePoint 管理中心，選取 [安全性]。  
  
2.  選取 [設定服務帳戶]。  
  
3.  選取 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式所使用的服務應用程式集區。 然後，選取 SPSvc 帳戶。  
  
 **若要使用 PowerShell，將存取權授與 Web 應用程式：**  
  
1.  使用系統管理員權限來執行 SharePoint 2016 管理命令介面。  
  
2.  執行下列 PowerShell 程式碼：  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  