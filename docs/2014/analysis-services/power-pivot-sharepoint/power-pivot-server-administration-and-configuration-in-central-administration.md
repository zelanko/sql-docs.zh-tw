---
title: 管理中心的 PowerPivot 伺服器管理和組態 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 62232430002833de70ecbf1cf76a401324b12174
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145498"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a>管理中心的 PowerPivot 伺服器管理和組態
  PowerPivot 伺服器管理與組態是由 SharePoint 服務應用程式管理員使用 SharePoint 管理中心所執行。  
  
 您必須先設定 PowerPivot for SharePoint，然後才能使用。 在您使用 SQL Server 安裝程式安裝 PowerPivot for SharePoint 之後，您可以使用下列任何方法加以設定：  
  
-   PowerPivot 組態工具或 PowerPivot for SharePoint 2013 組態工具  
  
-   SharePoint 管理中心  
  
-   PowerShell Cmdlet  
  
 這三種方法都提供完整設定的伺服器。  
  
 本節包含使用管理中心設定軟體的工作。 您至少必須執行底下清單所列的所有三個必要組態工作。  
  
> [!IMPORTANT]  
>  如果是 SharePoint 2010，您必須先安裝 SharePoint 2010 Service Pack 1 (SP1)，才可設定 PowerPivot for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 資料庫伺服器的 SharePoint 伺服器陣列。 如果您尚未安裝該 Service Pack，請在開始設定伺服器之前先加以安裝。  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a>使用管理中心設定 PowerPivot for SharePoint 的優點  
 SharePoint 管理中心是 SharePoint 伺服器陣列的管理應用程式。 如果您是伺服器陣列管理員，當您將 PowerPivot for SharePoint 執行個體加入至伺服器陣列時，可能會偏好使用熟悉的工具。  
  
 管理中心所提供的頁面會完整指定當您設定應用程式或伺服器時可能設定的所有選項，與 PowerPivot 組態工具或 PowerShell 指令程式相反。 其他方法會將組態工作流程濃縮成較少的步驟，或者需要事先了解如何使用 PowerShell 設定 SharePoint 伺服器。  
  
## <a name="related-content"></a>相關內容  
 [使用 Windows PowerShell 的 PowerPivot 組態](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot 組態工具](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>相關工作  
  
|連結|類型|工作描述|  
|----------|----------|----------------------|  
|[將 PowerPivot 方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)|必要項|這個步驟會安裝方案檔，這些檔案會將程式檔和應用程式頁面加入至伺服器陣列和網站集合。|  
|[建立並在管理中心設定 PowerPivot 服務應用程式](create-and-configure-power-pivot-service-application-in-ca.md)|必要項|這個步驟會佈建 PowerPivot 系統服務。|  
|[為在 [管理中心] 網站集合啟用 PowerPivot 功能整合](activate-power-pivot-integration-for-site-collections-in-ca.md)|必要項|這個步驟會在網站集合層級開啟 PowerPivot 功能。|  
|[將 MSOLAP.5 新增為 Excel Services 中信任的資料提供者](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|必要項|此步驟會加入 Analysis Services OLE DB 提供者做為 Excel Services 中受信任的提供者。|  
|[與 SharePoint 2010 的 PowerPivot 資料重新整理](../powerpivot-data-refresh-with-sharepoint-2010.md)|建議|資料重新整理為選擇性，但是建議使用它。 它可讓您將自動更新排程到已發行之 Excel 活頁簿中的 PowerPivot 資料。|  
|[設定 PowerPivot 無人看管的資料重新整理帳戶&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|建議|這個步驟會佈建特殊目的的帳戶，此帳戶可在伺服器上用來執行資料重新整理作業。|  
|[設定使用量資料收集的&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|選擇性|預設會設定使用量資料收集。 您可以使用這些步驟來修改預設值。|  
|[設定專用的資料重新整理或僅查詢處理&#40;PowerPivot for SharePoint&#41;](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|選擇性|PowerPivot 執行個體可以專門處理資料重新整理作業或查詢。 此外，您也可以修改平行資料重新整理作業的預設值。|  
|[設定 PowerPivot 服務帳戶](configure-power-pivot-service-accounts.md)|選擇性|說明如何更新密碼或變更服務帳戶。|  
|[在 [管理中心] 的 SharePoint Web 應用程式將 PowerPivot 服務應用程式連接](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|選擇性|說明如何修改服務關聯。|  
|[在管理中心建立 PowerPivot 網站的信任的位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|選擇性|說明如何將 PowerPivot 圖庫當做信任的位置加入。|  
|[設定及檢視 SharePoint 記錄檔與診斷記錄&#40;PowerPivot for SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)|選擇性|預設會設定事件記錄。 您可以使用這些步驟來修改預設值。|  
|[PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)|選擇性|預設會設定伺服器健全狀況規則。 您可以使用這些步驟來修改某些預設值。|  
|[建立及自訂 PowerPivot 圖庫](create-and-customize-power-pivot-gallery.md)|選擇性|如果是手動設定的安裝，這個程序會說明如何建立 PowerPivot 圖庫，以顯示其中所包含之 PowerPivot 活頁簿的影像縮圖。|  
|[將 BI 語意模型連接內容類型加入至文件庫&#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)|選擇性|說明如何擴充文件庫來支援 BI 語意模型連接檔案的建立。|  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot for SharePoint 2010 安裝](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [組態設定參考&#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Powerpivot for SharePoint 災害復原](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  