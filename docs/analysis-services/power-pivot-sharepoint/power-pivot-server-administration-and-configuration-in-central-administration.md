---
title: Power Pivot 伺服器系統管理和組態，在 [管理中心] |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e14e6068bc5d6538eab1ec13c3a3cc37ed34fb61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-server-administration-and-configuration-in-central-administration"></a>管理中心的 Power Pivot 伺服器管理和組態
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 伺服器管理與組態是由 SharePoint 服務應用程式管理員使用 SharePoint 管理中心所執行。  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint，然後才能使用。 在您使用 SQL Server 安裝程式安裝 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 之後，您可以使用下列任何方法加以設定：  
  
-   [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 組態工具或 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 2013 組態工具  
  
-   SharePoint 管理中心  
  
-   PowerShell Cmdlet  
  
 這三種方法都提供完整設定的伺服器。  
  
 本節包含使用管理中心設定軟體的工作。 您至少必須執行底下清單所列的所有三個必要組態工作。  
  
> [!IMPORTANT]  
>  如果是 SharePoint 2010，您必須先安裝 SharePoint 2010 Service Pack 1 (SP1)，才可設定 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 資料庫伺服器的 SharePoint 伺服器陣列。 如果您尚未安裝該 Service Pack，請在開始設定伺服器之前先加以安裝。  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-central-administration"></a>使用管理中心設定 PowerPivot for SharePoint 的優點  
 SharePoint 管理中心是 SharePoint 伺服器陣列的管理應用程式。 如果您是伺服器陣列管理員，當您將 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 執行個體加入伺服器陣列時，可能會偏好使用熟悉的工具。  
  
 管理中心所提供的頁面會完整指定當您設定應用程式或伺服器時可能設定的所有選項，與 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 組態工具或 PowerShell Cmdlet 相反。 其他方法會將組態工作流程濃縮成較少的步驟，或者需要事先了解如何使用 PowerShell 設定 SharePoint 伺服器。  
  
## <a name="related-content"></a>相關內容  
 [使用 Windows PowerShell 的 Power Pivot 組態](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [Power Pivot 組態工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>相關工作  
  
|連結|型別|工作描述|  
|----------|----------|----------------------|  
|[將 Power Pivot 方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)|必要項|這個步驟會安裝方案檔，這些檔案會將程式檔和應用程式頁面加入至伺服器陣列和網站集合。|  
|[在管理中心建立和設定 Power Pivot 服務應用程式](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)|必要項|這個步驟會佈建 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 系統服務。|  
|[在管理中心為網站集合啟用 Power Pivot 功能整合](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|必要項|這個步驟會在網站集合層級開啟 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 功能。|  
|[加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|必要項|此步驟會加入 Analysis Services OLE DB 提供者做為 Excel Services 中受信任的提供者。|  
|[SharePoint 2010 中的 PowerPivot 資料重新整理](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)|建議|資料重新整理為選擇性，但是建議使用它。 它可讓您將自動更新排程到已發行之 Excel 活頁簿中的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 資料。|  
|[設定 Power Pivot 自動資料重新整理帳戶 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)|建議|這個步驟會佈建特殊目的的帳戶，此帳戶可在伺服器上用來執行資料重新整理作業。|  
|[設定使用量資料收集的對象 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|選擇性|預設會設定使用量資料收集。 您可以使用這些步驟來修改預設值。|  
|[設定專用的資料重新整理或僅查詢處理 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/5e027605-1086-4941-bb01-f315df8f829b)|選擇性|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 執行個體可以專門處理資料重新整理作業或查詢。 此外，您也可以修改平行資料重新整理作業的預設值。|  
|[設定 Power Pivot 服務帳戶](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)|選擇性|說明如何更新密碼或變更服務帳戶。|  
|[在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|選擇性|說明如何修改服務關聯。|  
|[在管理中心建立 Power Pivot 網站的信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|選擇性|說明如何將 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 圖庫當做信任的位置加入。|  
|[設定及檢視 SharePoint 記錄檔與診斷記錄 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)|選擇性|預設會設定事件記錄。 您可以使用這些步驟來修改預設值。|  
|[設定 Power Pivot 健康情況規則](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)|選擇性|預設會設定伺服器健全狀況規則。 您可以使用這些步驟來修改某些預設值。|  
|[建立及自訂 Power Pivot 圖庫](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)|選擇性|如果是手動設定的安裝，這個程序會說明如何建立 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 圖庫，以顯示其中所包含之 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 活頁簿的影像縮圖。|  
|[將 BI 語意模型連接內容類型加入至文件庫 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)|選擇性|說明如何擴充文件庫來支援 BI 語意模型連接檔案的建立。|  
  
## <a name="see-also"></a>另請參閱  
 [Power Pivot for SharePoint 2010 安裝](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [組態設定參考 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Power pivot for SharePoint 災害復原](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
