---
title: "連接到表格式模型資料庫 (SSAS) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 983d0c8a-77da-4c6e-8638-283bcb14f143
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85963e947dbed1fc2d1574a537d0e42f61fbba35
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="connect-to-a-tabular-model-database-ssas"></a>連接到表格式模型資料庫 (SSAS)
  建置表格式模型，並將其部署到 Analysis Services 表格式模式伺服器之後，您需要設定權限，使其可供用戶端應用程式使用。 此主題說明如何設定權限和如何從用戶端應用程式連接到資料庫。  
  
> [!NOTE]  
>  根據預設，在設定防火牆之前，無法使用 Analysis Services 的遠端連接。 如果您要為用戶端連接設定具名或預設的執行個體，請確認您已經開放適當的連接埠。 如需詳細資訊，請參閱 [設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
 本主題包含下列幾節：  
  
 [資料庫的使用者權限](#bkmk_userpermissions)  
  
 [伺服器的管理權限](#bkmk_admin)  
  
 [從 Excel 或 SharePoint 連接](#bkmk_excelconn)  
  
 [連接問題的疑難排解](#bkmk_Tshoot)  
  
##  <a name="bkmk_userpermissions"></a> 資料庫的使用者權限  
 連接到在表格式資料庫的使用者必須擁有指定讀取權限的資料庫角色成員資格。  
  
 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中撰寫模型時定義角色，對於已部署的模型，則透過使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 定義角色，有時也要定義角色成員資格。 如需使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中的角色管理員建立角色的詳細資訊，請參閱[建立及管理角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。 如需為已部署的模型建立及管理角色的詳細資訊，請參閱[表格式模型角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)。  
  
> [!CAUTION]  
>  透過在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中使用 [角色管理員] 定義的角色重新部署表格式模型專案，將會覆寫已部署表格式模型中定義的角色。  
  
##  <a name="bkmk_admin"></a> 伺服器的管理權限  
 對於使用 SharePoint 來裝載 Excel 活頁簿或 Reporting Services 報表的組織，需要其他設定，才能將表格式模型資料提供給 SharePoint 使用者。 如果您並未使用 SharePoint，請略過本節。  
  
 用來執行 Excel Services 或 Reporting Services 的帳戶需要擁有 Analysis Services 執行個體的系統管理員權限，才能檢視包含表格式資料的 Excel 活頁簿或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表。 需要管理員權限，Analysis Services 執行個體才會信任這些服務。  
  
#### <a name="grant-administrative-access-on-the-server"></a>授與伺服器的管理存取權限  
  
1.  在「管理中心」內，開啟 [設定服務帳戶] 頁面。  
  
2.  選取 Excel Services 所使用的服務應用程式集區。 它可能是 [服務應用程式集區 - SharePoint Web 服務系統] 或自訂應用程式集區。 Excel Services 所使用的受管理帳戶將會出現在此頁面上。  
  
     如果 SharePoint 伺服器陣列包含 SharePoint 模式的 Reporting Services，也要取得 Reporting Services 服務應用程式的帳戶資訊。  
  
     在下列步驟中，您會將這些帳戶加入至 Analysis Services 執行個體上的伺服器角色。  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，以滑鼠右鍵按一下此伺服器執行個體，然後選取 [屬性]。 在物件總管中，以滑鼠右鍵按一下 [角色]，然後選取 [新增角色]。  
  
4.  在 [Analysis Services 屬性] 頁面中，按一下 [安全性]。  
  
5.  按一下 [加入]，然後輸入 Excel Service 所使用的帳戶，後面接著 Reporting Services 所使用的帳戶。  
  
##  <a name="bkmk_excelconn"></a> 從 Excel 或 SharePoint 連接  
 提供 Analysis Services 資料庫存取權的用戶端程式庫可以用來連接到在表格式模式伺服器上執行的模型資料庫。 程式庫包含 Analysis Services OLE DB 提供者、ADOMD.NET 和 AMO。  
  
 Excel 使用 OLE DB 提供者。 如果您有來自 SQL Server 2008 R2 的 MSOLAP.4 (檔案名稱為 msolap100.dll，10.50.1600.1 版)，或與 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 一起安裝的 MSOLAP.5 (檔案名稱為 msolap110.dll)，您就有將連接至表格式資料庫的版本。  
  
 請從下列連接至 Excel 中之模型資料庫的方法中進行選擇：  
  
-   使用下一節中提供的指示，從 Excel 中建立資料連接。  
  
-   在 SharePoint 中，建立 BI 語意模型連接 (.bism) 檔案，這個檔案會重新導向至 Analysis Services 表格式模式伺服器上執行的資料庫。 BI 語意模型連接檔案提供一個滑鼠右鍵的命令，可使用您在連接中指定的模型資料庫啟動 Excel。 如果安裝了 Reporting Services，它也會啟動 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 。 如需建立及使用 BI 語意模型連接檔案的詳細資訊，請參閱 [建立與表格式模型資料庫的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
-   建立將表格式資料庫做為資料來源參考的 Reporting Services 共用資料來源。 您可以在 SharePoint 中建立共用資料來源，並且使用該資料來源啟動 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。  
  
#### <a name="connect-from-excel"></a>從 Excel 連接  
  
1.  在 Excel 的 [資料] 索引標籤上，按一下 [取得外部資料] 中的 [從其他來源]。  
  
2.  選取 [從 Analysis Services]。  
  
3.  在 [伺服器名稱] 中，指定裝載資料庫的 Analysis Services 執行個體。 伺服器名稱通常是執行伺服器軟體之電腦的名稱。 如果伺服器已安裝成具名執行個體，您必須以此格式指定名稱： \<servername >\\< instancename\>。  
  
     您必須針對獨立的表格式部署設定伺服器執行個體，而且伺服器執行個體必須有允許存取的輸入規則。 如需詳細資訊，請參閱[判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)和[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
4.  對於登入認證，如果您有資料庫的讀取權限，請選擇 [使用 Windows 驗證]。 否則，請選擇 [使用下列的使用者名稱和密碼]，然後輸入具有資料庫權限之 Windows 帳戶的使用者名稱和密碼。 按一下 **[下一步]**。  
  
5.  選取資料庫。 有效的選項將會針對資料庫顯示一個 [模型] Cube。 按一下 [下一步]，然後按一下 [完成]。  
  
 建立連接之後，您可以使用資料來建立樞紐分析表或樞紐分析圖。 如需詳細資訊，請參閱本主題稍後的 [在 Excel 中進行分析 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)中的 [角色管理員] 對話方塊來定義角色的表格式模型作者。  
  
##  <a name="bkmk_sharepoint"></a> 從 SharePoint 連接  
 如果您要使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，可以在 SharePoint 中建立 BI 語意模型連接檔案，這個檔案會重新導向至 Analysis Services 表格式模式伺服器上執行的資料庫。 BI 語意模型連接會提供 HTTP 端點給資料庫。 它也會針對例行使用 SharePoint 網站之文件的知識工作者，簡化表格式模型存取。 知識工作者只需要知道 BI 語意模型連接檔案的位置或其 URL，就可以存取表格式模型資料庫。 關於伺服器位置或資料庫名稱的詳細資料，都會封裝在 BI 語意模型連接中。 如需建立及使用 BI 語意模型連接檔案的詳細資訊，請參閱 [Power Pivot BI 語意模型連接 &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md) 和[建立與表格式模型資料庫的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
##  <a name="bkmk_Tshoot"></a> 連接問題的疑難排解  
 本節提供連接到表格式模型資料庫時發生之問題的原因和解決步驟。  
  
 **「資料連線精靈」無法從指定的資料來源取得資料庫清單。**  
  
 匯入資料時，如果您嘗試使用此精靈連接到遠端 Analysis Services 伺服器上的表格式模型資料庫，而且您沒有足夠的權限，就會發生這個 Microsoft Excel 錯誤。 若要解決這個錯誤，您必須擁有資料庫的使用者存取權限。 如需授與使用者對資料的存取權，請參閱本主題稍早所提供的指示。  
  
 **嘗試建立與外部資料來源之間的連接時，發生錯誤。下列連接無法重新整理：\<模型名稱 > 沙箱**  
  
 在 SharePoint 上，當您嘗試使用模型資料之樞紐分析表中的資料互動 (如篩選資料) 時，就會發生這個 Microsoft Excel 錯誤。 此錯誤的發生，是因為您在遠端 Analysis Services 伺服器上沒有足夠的權限。 若要解決這個錯誤，您必須擁有資料庫的使用者存取權限。 如需授與使用者對資料的存取權，請參閱本主題稍早所提供的指示。  
  
 **嘗試執行此作業時發生錯誤。重新載入活頁簿，並嘗試再次執行此作業。**  
  
 在 SharePoint 上，當您嘗試使用模型資料之樞紐分析表中的資料互動 (如篩選資料) 時，就會發生這個 Microsoft Excel 錯誤。 此錯誤發生的原因，是因為部署模型資料所在的 Analysis Services 執行個體不信任 Excel Services。 若要解決這個錯誤，請在 Analysis Services 執行個體上，授與 Excel Services 管理權限。 如需授與系統管理員權限，請參閱本主題稍早所提供的指示。 如果錯誤仍然存在，請回收 Excel Services 應用程式集區。  
  
 **嘗試建立與活頁簿中所使用之外部資料來源間的連接時，發生錯誤。**  
  
 在 SharePoint 上，當您嘗試使用模型資料之樞紐分析表中的資料互動 (如篩選資料) 時，就會發生這個 Microsoft Excel 錯誤。 此錯誤的發生，是因為使用者在活頁簿上沒有足夠的 SharePoint 權限。 使用者必須具有 [讀取] (含) 以上的權限。 [僅供檢視] 權限不足以進行資料存取。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型方案部署 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
