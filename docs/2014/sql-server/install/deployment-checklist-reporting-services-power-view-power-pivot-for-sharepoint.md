---
title: 部署檢查清單：Reporting Services、 Power View 及 PowerPivot for SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 9a2575c8-06fc-4ef4-9f24-c19e52b1bbcf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2aa1133b9e23ea8f2174f73e9d8bf4a34ff0c824
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369100"
---
# <a name="deployment-checklist-reporting-services-power-view-and-powerpivot-for-sharepoint"></a>部署檢查清單：Reporting Services、Power View 及 PowerPivot for SharePoint
  使用下列檢查清單在相同的 SharePoint 伺服器陣列中安裝這些 BI 功能：PowerPivot for SharePoint、報表產生器及 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。 雖然此檢查清單建議特定的安裝順序，但是在練習時，您可以幾乎任何順序來安裝這些功能。 此檢查清單假設已安裝下列產品或功能：  
  
1.  SharePoint Server 2010 Service Pack 1 (SP1)  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 資料庫引擎  
  
3.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 和 Reporting Services 增益集  
  
4.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint  
  
 安裝這些功能之後，即可執行下列作業。  
  
-   從 SharePoint 網站存取您在 PowerPivot for Excel 中建立的 PowerPivot 活頁簿。  
  
-   根據 SharePoint 的 PowerPivot 活頁簿，建立互動式 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表。  
  
-   在 SharePoint 中啟動報表產生器時，建立報表產生器報表。  
  
> [!NOTE]  
>  PowerPivot for SharePoint 要求您在 SharePoint 伺服器陣列上安裝 SharePoint 2010 Service Pack 1 (SP1)。 如果您基於評估目的安裝軟體，請考慮從全新的伺服器開始進行，以避免伺服器陣列升級步驟的負擔。 升級伺服器陣列會影響 SharePoint 作業，因此通常需要謹慎規劃。 如果您的目標在於儘快安裝 PowerPivot for SharePoint，請遵循此方法：安裝 SharePoint 2010、安裝 SharePoint 2010 SP1，然後在之後的步驟中設定伺服器陣列。 當您安裝 SharePoint 2010 SP1 時，尚未設定伺服器陣列，因此請避免升級。  
>   
>  在此檢查清單中，會假設在 PowerPivot for SharePoint 設定期間，使用 PowerPivot 組態工具進行伺服器陣列的設定步驟。 或者，您可以使用「SharePoint 產品設定」精靈 (如果您慣用該方法)。 這兩種方法都會導致支援 PowerPivot for SharePoint 的伺服器陣列正常運作。  
  
## <a name="prerequisites"></a>先決條件  
 您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
 PowerPivot for SharePoint 需要 SharePoint Server 2010 Enterprise 版。 您也可以使用 Evaluation Enterprise 版。  
  
 您必須安裝 SharePoint Server 2010 SP1。 若未安裝，則無法設定伺服器陣列使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 功能。  
  
 電腦必須加入網域。  
  
 您必須擁有一個或多個網域使用者帳戶，才能佈建服務。 下列服務需要網域使用者帳戶：SharePoint Web 服務和系統管理服務、Reporting Services、Analysis Services、Excel Services、Secure Store Services 及 PowerPivot 系統服務。 SharePoint 的受管理帳戶功能需要網域帳戶。 您可以使用虛擬帳戶佈建 Database Engine，但是其他所有服務應以網域使用者的身分執行。  
  
 必須提供 PowerPivot 執行個體名稱。 您無法於正在安裝 PowerPivot for SharePoint 的電腦上，具有現存的 PowerPivot 具名執行個體。  
  
 若您正在現有的伺服器陣列上安裝 PowerPivot for SharePoint，必須要有一個或多個為傳統模式驗證所設定的 SharePoint Web 應用程式。 只有當 Web 應用程式支援傳統模式驗證時，PowerPivot 資料存取才有功能。 如需有關傳統模式需求的詳細資訊，請參閱 < [PowerPivot 驗證及授權](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md)。  
  
 請檢閱下列其他主題，以了解系統與版本需求：  
  
-   [在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>步驟  
 下列步驟假設管理員要安裝及設定伺服器。 SharePoint 的安裝程式使用者同時也是伺服器陣列管理員，且通常是預設網站集合的主要網站管理員。 如果您將下列步驟分配給多位人員，可能需要其他權限才能執行下列步驟。  
  
|步驟|連結|  
|----------|----------|  
|執行 SharePoint 2010 產品準備工具|您必須擁有 SharePoint 2010 安裝媒體。 準備工具是安裝媒體上的 PrerequisiteInstaller.exe。|  
|安裝 SharePoint Server 2010 Enterprise Edition 或 Enterprise Evaluation Edition。|安裝 SharePoint 時，您可以選擇在完成安裝程式之後，不要執行 [SharePoint 2010 產品設定精靈]，以在稍後設定伺服器陣列。 等候設定伺服器陣列可讓您使用[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Database Engine 執行個體，這會安裝在稍後的步驟中，做為伺服器陣列的資料庫伺服器。 若要設定伺服器陣列，請使用 PowerPivot 組態工具。 此工具包括佈建尚未設定之伺服器陣列的動作。|  
|安裝 SharePoint Server 2010 SP1。|下載從 SP1 [ https://support.microsoft.com/kb/2460045 ](https://go.microsoft.com/fwlink/p/?linkID=219697)。|  
|執行 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安裝程式，以安裝 Database Engine 和 PowerPivot for SharePoint。|[安裝 PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 步驟 1 說明如何安裝 PowerPivot for SharePoint。 在此步驟中，請務必按一下 [安裝程式角色] 頁面上的核取方塊，以將 Database Engine 加入角色。 如此一來您的安裝將 Database Engine，好讓您可以使用它做為伺服器陣列的資料庫伺服器在下一個步驟中設定伺服器陣列時。 不過，如果已經設定伺服器陣列，您就可以略過此步驟。<br /><br /> 步驟 2 要求您設定伺服器。 在此步驟中，請選擇 PowerPivot 組態工具。 雖然有許多方法可用，但是使用組態工具是對獨立安裝最有效率的方法。<br /><br /> 如果安裝 SharePoint 2010 但未設定，此工具會預先選取動作，以建立伺服器陣列、預設 Web 應用程式及根網站集合。 請務必保留選取這些選項，以建立伺服器陣列。 如果您已經設定伺服器陣列，此工具會省略這些動作，只提供設定 PowerPivot for SharePoint 的必要動作。<br /><br /> 步驟 3 指示您安裝 SQL Server 2008 R2 版的 Analysis Services OLE DB 提供者。 此步驟對於支援在 2008 R2 版的 PowerPivot for Excel 中建立之活頁簿版本而言很重要。|  
|確認伺服器陣列可以運作。|首先，啟動管理中心並確認可以使用。 接下來，輸入以開啟小組網站 http://localhost。  您應該會看到 SharePoint 小組網站。|  
|確認 PowerPivot for SharePoint 可以運作。|[確認 PowerPivot for SharePoint 安裝](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)<br /><br /> 此工作使用您上傳的範例活頁簿確認 PowerPivot 資料存取。|  
|執行 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安裝程式，以安裝及設定 Reporting Services 和 Reporting Services 增益集。|[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)<br /><br /> 如果您需要第二個資源來裝載表格式資料，您也可以在安裝 Reporting Services 時，選擇將額外的 Analysis Services 執行個體加入安裝功能樹狀目錄。 此額外的 Analysis Services 執行個體可用來裝載您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中建立的表格式模型資料庫。 表格式資料庫是 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表的有效資料來源。<br /><br /> [以表格式模式安裝 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)|  
|確認 Reporting Services 可以運作。|[驗證 Reporting Services 安裝](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
|(網站管理員) 設定 SharePoint 權限。|在 SharePoint 文件庫中加入、編輯或刪除項目需要「參與」權限。 若要唯讀存取呈現內嵌資料的報表和 PowerPivot 活頁簿，「檢視」權限等級便已足夠。<br /><br /> 做為外部資料來源存取的 PowerPivot 活頁簿 (活頁簿 URL 是其他活頁簿或報表的連接字串) 需要比「檢視」權限更高的「讀取」權限。<br /><br /> BI 語意模型連接也需要「讀取」權限。 您可能需要建立新的權限等級或 SharePoint 群組，以取得正確的權限。|  
|(網站管理員) 擴充文件庫|擴充文件庫以使用 BI 內容類型：BI 語意模型連接、Reporting Services 共用資料來源、報表產生器報表：<br /><br /> 1) <br />                    **啟用內容類型管理**。 在共用文件或其他文件庫，在 程式庫 索引標籤中，按一下 **文件庫設定**。 一般設定 下按一下 **進階設定**。 在 內容類型選取**是**以允許管理內容類型，然後按一下**確定**。<br /><br /> 2) <br />                    **選取 BI 內容類型**。 在 [程式庫] 索引標籤中，按一下**文件庫設定**。 在 內容類型，按一下**從現有的網站內容類型新增**。 從商業智慧 內容類型群組中，新增**BI 語意模型連接檔案**並**報表資料來源**。 您也可以選擇加入其他 Reporting Services 內容類型 (例如報表模型)，以啟用其他報表建立案例。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 <<c0> [ 將 BI 語意模型連接內容類型加入至文件庫&#40;PowerPivot for SharePoint&#41; ](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)並[將報表伺服器內容類型加入至文件庫&#40;中的 Reporting ServicesSharePoint 整合模式&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。</c0>|  
|(網站管理員) 建立用來啟動 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 的資料連接檔案。|您必須建立 BI 語意模型連接 (.bism) 或 Reporting Services 共用資料來源 (.rsds)，做為 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 的資料來源。 建立資料連接檔案之後，即可使用資料連接做為資料來源以啟動 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。<br /><br /> [建立與 PowerPivot 活頁簿的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)<br /><br /> [C建立與表格式模型資料庫的 BI 語意模型連接](../../relational-databases/databases/model-database.md)<br /><br /> 注意：由於您已安裝 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 版的 Reporting Services 並將伺服器設定為共用服務，因此可以使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。 如果您安裝 Reporting Services 並針對 SQL Server 2008 整合層級設定 Reporting Services，則無法使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473)  
  
  
