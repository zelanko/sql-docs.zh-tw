---
title: "將其他 Reporting Services Web 前端新增至伺服器陣列 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
caps.latest.revision: "11"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: cfbfe817bb6978527f2604832da610d2623dc7a4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>將其他 Reporting Services Web 前端加入至伺服器陣列
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式包含應用程式伺服器和 Web 前端 (WFE) 伺服器所需的元件。 本主題的重點在於安裝 WFE 伺服器的必要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能所使用的應用程式頁面，例如訂閱、資料警示和 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。 WFE 所需的主要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝是安裝適用於 SharePoint 2016 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。  
  
## <a name="prerequisites"></a>必要條件  
  
-   您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
-   電腦必須加入網域。  
  
-   您必須知道裝載 SharePoint 組態和內容資料庫之現有資料庫伺服器的名稱。  
  
-   資料庫伺服器必須設定為允許遠端資料庫連接。  如果不允許，您就無法將新的伺服器加入伺服器陣列，因為新的伺服器將無法建立 SharePoint 組態資料庫的連接。  
  
-   新的伺服器必須安裝目前伺服器陣列伺服器所執行的相同 SharePoint 版本。 例如，如果伺服器陣列已經安裝 SharePoint 2013 Service Pack 1 (SP1)，您也必須在新的伺服器上安裝 SP1，才能讓它加入伺服器陣列。  
  
## <a name="steps"></a>步驟  
 本主題中的步驟假設 SharePoint 伺服器陣列管理員要安裝及設定伺服器。 下圖顯示一般三層環境，而且下圖中的編號項目將於下列清單中描述：  
  
-   (1) 多個 Web 前端 (WFE) 伺服器。 WFE 伺服器需要適用於 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 下列步驟會將第二個應用程式伺服器加入至這一層。  
  
-   (2) 執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和網站的兩個應用程式伺服器，例如管理中心。  
  
-   (3) 兩個 SQL Server 資料庫伺服器。  
  
-   (4) 代表軟體或硬體網路負載平衡解決方案 (NLB)。  
  
 ![將 SSRS 新增至新的 SharePoint WFE](../../reporting-services/install-windows/media/rs-sharepointscale-wfe.gif "將 SSRS 新增至新的 SharePoint WFE")  
  
 下列步驟假設管理員要安裝及設定伺服器。  
  
|步驟|說明和連結|  
|----------|--------------------------|  
|將 SharePoint 伺服器加入伺服器陣列中。|您需安裝 SharePoint 以部署其他 Reporting Services 應用程式。<br/><br/>若是 SharePoint 2013，請參閱 [Add SharePoint server to a farm in SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)(在 SharePoint Server 2013 中將 SharePoint 伺服器加入伺服陣列)。<br/><br/>若是 SharePoint 2016，請參閱 [Add SharePoint server to a farm in SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)(在 SharePoint Server 2016 中將 SharePoint 伺服器加入伺服陣列)。|  
|安裝適用於 SharePoint 2016 產品的 SQL Server Reporting Services 增益集。|安裝此增益集的方法有許多種。 下列步驟會使用 SQL Server 安裝精靈。 如需有關安裝增益集的詳細資訊，請參閱 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。<br /><br /> 1) 執行 SQL Server 安裝。<br /><br /> 2) 在 [安裝程式角色] 頁面上，選取 [SQL Server 功能安裝]。<br /><br /> 3) 在 [特徵選取] 頁面上，選取 [適用於 SharePoint 產品的 Reporting Services 增益集]<br /><br /> 4) 在後續許多頁面上，按一下 [下一步] 完成安裝選項。<br /><br/>如需有關安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的詳細資訊，請參閱 [在 SharePoint 模式中安裝第一部報表伺服器](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538)。|  
|確認新的伺服器可以運作。|1) 在 SharePoint 管理中心內，按一下 [系統設定] 群組中的 [管理此伺服器陣列中的伺服器]。<br /><br /> 2) 確認新的伺服器位於清單中。|  
|更新您的 NLB 解決方案。|依照適當的情況，將您的硬體或軟體 NLB 環境更新為包含新的伺服器。|  

## <a name="next-steps"></a>後續的步驟

[Add SharePoint server to a farm in SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[Add SharePoint server to a farm in SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
