---
title: Powerpivot for SharePoint 2013 的最低權限組態範例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f24ee3e02daaaa906c8285cd6d78dacb9973c6ac
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079893"
---
# <a name="example-of-a-minimum-privilege-configuration-for-powerpivot-for-sharepoint-2013"></a>PowerPivot for SharePoint 2013 的最低權限組態範例
  本主題描述具有最低權限的 PowerPivot for SharePoint 2013 組態範例。 此組態會分別針對三個元件使用不同的帳戶，而且每個帳戶都具有最低層級的權限。  
  
## <a name="summary-of-accounts"></a>帳戶摘要  
 PowerPivot for SharePoint 2013 支援使用網路服務帳戶做為 Analysis Services 服務帳戶。 網路服務帳戶並非 SharePoint 2010 的支援案例。 如需有關服務帳戶的詳細資訊，請參閱 <<c0> [ 設定 Windows 服務帳戶與權限](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)(https://msdn.microsoft.com/library/ms143504.aspx)。  
  
 下表將摘要說明用於這個最低權限組態範例的三個帳戶。  
  
|範圍。|名稱|  
|-----------|----------|  
|SharePoint 管理員帳戶|**SPAdmin**|  
|SharePoint 伺服器陣列帳戶|**SPFarm**|  
|Analysis Services 服務帳戶|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>SharePoint 管理員帳戶 (SpAdmin)  
 **SPAdmin** 是您用來安裝和設定伺服器陣列的網域帳戶。 它是用來執行 SharePoint 組態精靈] 和 [適用於 SharePoint 2013 的 PowerPivot 組態工具的帳戶**SPAdmin**帳戶是唯一需要本機系統管理員權限的帳戶。 執行 PowerPivot 組態工具之前，授與**SPAdmin**帳戶，其為 SharePoint 建立內容和組態資料庫的 SQL Server 資料庫執行個體的權限。 若要在最低權限案例中設定 SPAdmin 帳戶，它必須是 **securityadmin** 和 **dbcreator**角色的成員。  
  
### <a name="the-farm-account-spfarm"></a>伺服器陣列帳戶 (SPFarm)  
 **SPFarm** 是 SharePoint Timer Service 和管理中心 Web 應用程式用來存取 SharePoint 內容資料庫的網域帳戶。 這個帳戶不需要是本機系統管理員。 [SharePoint 組態精靈] 會授與後端 SQL Server 資料庫的適當最低權限。最低 SQL Server 權限組態就是 **securityadmin** 和 **dbcreator**角色的成員資格。  
  
### <a name="the-service-account-for-powerpivot-service-spsvc"></a>PowerPivot 服務的服務帳戶 (SPsvc)  
 如果您沒有在執行 PowerPivot 組態工具之前設定新的 SharePoint 伺服器陣列，則 PowerPivot 組態工具預設將建立下列項目：  
  
-   PowerPivot 服務應用程式。  
  
-   Excel Services 應用程式。  
  
-   安全存放應用程式。  
  
 PowerPivot 組態工具會在預設應用程式集區中設定這三個服務應用程式。 該應用程式集區通常設定為以 SPFarm 帳戶的身分執行，這個帳戶可存取服務帳戶不需要的許多資源。若要讓環境成為最低權限的環境，請設定要由適當應用程式集區和 Web 應用程式使用的新網域帳戶。  
  
 **若要建立要當做 SharePoint 服務帳戶使用的新網域帳戶 SPsvc：**  
  
1.  在 SharePoint 管理中心內，按一下**安全性**。  
  
2.  按一下 **設定服務帳戶**  
  
3.  按一下 **註冊新的受控帳戶**。  
  
 **SPSvc** 帳戶沒有任何本機系統管理員權限，而且 SPsvc 沒有 SharePoint 資料庫的任何權限。 SPsvc 所需的唯一權限就是 Analysis Services 之 PowerPivot 執行個體的管理權限。  
  
 **若要將適當的應用程式集區設定為使用 SPsvc 帳戶：**  
  
1.  在 SharePoint 管理中心內，按一下**安全性**。  
  
2.  按一下 **來設定服務帳戶**。  
  
3.  選取 PowerPivot 服務應用程式所使用的服務應用程式集區。 然後，選取 SPSvc 帳戶。  
  
 **若要使用 PowerShell，將存取權授與 Web 應用程式：**  
  
1.  使用系統管理員權限來執行 SharePoint 2013 管理命令介面。  
  
2.  執行下列 PowerShell 程式碼：  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
