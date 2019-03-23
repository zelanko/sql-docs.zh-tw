---
title: 新增、 刪除或共用封裝中的連線管理員 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdcc6285ba1a75827f91f856319d296c0cbbff5d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391686"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>加入、刪除或共用封裝中的連接管理員
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括用來連接到其他資料來源 (例如，關聯式資料庫、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，以及 CSV 和 XML 格式的檔案) 的各種連線管理員類型。 您可以在封裝層級或專案層級建立連接管理員。 在專案層級建立的連接管理員可在專案中的所有封裝上使用。 而在封裝層級建立的連接管理員則可在該特定封裝上使用。  
  
 您將使用在專案層級建立的連接管理員取代資料來源，以共用來源的連接。 若要在專案層級加入連接管理員，則 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案必須使用專案部署模型。 當專案設定為使用該模型時，[連線管理員] 資料夾會出現在方案總管中，而 [資料來源] 資料夾則會從方案總管移除。  
  
> [!NOTE]  
>  若您想使用封裝中的資料來源，便需要將專案轉換為封裝部署模型。  
>   
>  如需兩個模型的詳細資訊，請參閱 [部署專案和封裝](packages/deploy-integration-services-ssis-projects-and-packages.md)。 如需將專案轉換為專案部署模型的詳細資訊，請參閱 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
 下列程序適用於所有類型的連接管理員，並描述如何執行以下工作：  
  
-   [若要建立封裝時加入連接管理員](#wizard)  
  
-   [若要將連接管理員加入至現有的封裝](#package)  
  
-   [若要在專案層級加入連接管理員](#project)  
  
-   [若要建立連線管理員屬性的參數](#parameter)  
  
-   [若要從封裝中刪除連接管理員](#DeletePackageLevel)  
  
-   [若要刪除共用的連接管理員 （專案層級的連接管理員）](#DeleteProjectLevel)  
  
##  <a name="wizard"></a> 若要建立封裝時加入連接管理員  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈  
  
     除了建立及設定連接管理員之外，此精靈也會協助您建立及設定使用此連接管理員的來源和目的地。 如需詳細資訊，請參閱 [在 SQL Server 資料工具中建立封裝](create-packages-in-sql-server-data-tools.md)。  
  
##  <a name="package"></a> 若要將連接管理員加入至現有的封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [控制流程] 索引標籤、[資料流程] 索引標籤或 [事件處理常式] 索引標籤，以讓 [連線管理員] 區域可用。  
  
4.  以滑鼠右鍵按一下 [連線管理員] 區域的任意位置，然後執行下列其中之一：  
  
    -   按一下要加入封裝的連接管理員類型。  
  
         -或-  
  
    -   如果未列出要加入的類型，請按一下 [新增連接]，以開啟 [加入 SSIS 連線管理員] 對話方塊、選取連線管理員類型，然後按一下 [確定]。  
  
     已選取連接管理員類型的自訂對話方塊隨即開啟。 如需有關連接管理員類型和可用選項的詳細資訊，請參閱下列選項表。  
  
    |[ODBC 來源編輯器]|選項。|  
    |------------------------|-------------|  
    |[ADO 連線管理員](connection-manager/ado-connection-manager.md)|[設定 OLE DB 連線管理員](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 連線管理員](connection-manager/ado-net-connection-manager.md)|[設定 ADO.NET 連線管理員](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 連線管理員](connection-manager/analysis-services-connection-manager.md)|[加入 Analysis Services 連線管理員對話方塊 UI 參考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 連線管理員](connection-manager/excel-connection-manager.md)|[Excel 連線管理員編輯器](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[檔案連線管理員](connection-manager/file-connection-manager.md)|[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[多重檔案連線管理員](connection-manager/multiple-files-connection-manager.md)|[加入檔案連線管理員對話方塊 UI 參考](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[一般檔案連線管理員](connection-manager/flat-file-connection-manager.md)|[一般檔案連線管理員編輯器 &#40;[一般]頁面&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [一般檔案連接管理員編輯器 &#40;[預覽] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[多重一般檔案連線管理員](connection-manager/multiple-flat-files-connection-manager.md)|[多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 連線管理員](connection-manager/ftp-connection-manager.md)|[FTP 連線管理員編輯器](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 連線管理員](connection-manager/http-connection-manager.md)|[HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 連線管理員](connection-manager/msmq-connection-manager.md)|[MSMQ 連線管理員編輯器](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 連線管理員](connection-manager/odbc-connection-manager.md)|[ODBC 連線管理員 UI 參考](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 連線管理員](connection-manager/ole-db-connection-manager.md)|[設定 OLE DB 連線管理員](configure-ole-db-connection-manager.md)|  
    |[SMO 連線管理員](connection-manager/smo-connection-manager.md)|[SMO 連線管理員編輯器](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 連線管理員](connection-manager/smtp-connection-manager.md)|[SMTP 連線管理員編輯器](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 連線管理員](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 連線管理員](connection-manager/wmi-connection-manager.md)|[WMI 連線管理員編輯器](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     [連線管理員] 區域會列出加入的連線管理員。  
  
5.  選擇性地以滑鼠右鍵按一下連線管理員，並按一下 [重新命名]，然後修改連線管理員的預設名稱。  
  
6.  若要儲存更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
##  <a name="project"></a> 若要在專案層級加入連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [連線管理員]，然後按一下 [新增連線管理員]。  
  
3.  在 [加入 SSIS 連線管理員] 對話方塊中，選取連線管理員的類型，然後按一下 [加入]。  
  
     已選取連接管理員類型的自訂對話方塊隨即開啟。 如需有關連接管理員類型和可用選項的詳細資訊，請參閱下列選項表。  
  
    |[ODBC 來源編輯器]|選項。|  
    |------------------------|-------------|  
    |[ADO 連線管理員](connection-manager/ado-connection-manager.md)|[設定 OLE DB 連線管理員](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 連線管理員](connection-manager/ado-net-connection-manager.md)|[設定 ADO.NET 連線管理員](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 連線管理員](connection-manager/analysis-services-connection-manager.md)|[加入 Analysis Services 連線管理員對話方塊 UI 參考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 連線管理員](connection-manager/excel-connection-manager.md)|[Excel 連線管理員編輯器](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[檔案連線管理員](connection-manager/file-connection-manager.md)|[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[多重檔案連線管理員](connection-manager/multiple-files-connection-manager.md)|[加入檔案連線管理員對話方塊 UI 參考](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[一般檔案連線管理員](connection-manager/flat-file-connection-manager.md)|[一般檔案連線管理員編輯器 &#40;[一般]頁面&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [一般檔案連接管理員編輯器 &#40;[預覽] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[多重一般檔案連線管理員](connection-manager/multiple-flat-files-connection-manager.md)|[多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 連線管理員](connection-manager/ftp-connection-manager.md)|[FTP 連線管理員編輯器](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 連線管理員](connection-manager/http-connection-manager.md)|[HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 連線管理員](connection-manager/msmq-connection-manager.md)|[MSMQ 連線管理員編輯器](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 連線管理員](connection-manager/odbc-connection-manager.md)|[ODBC 連線管理員 UI 參考](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 連線管理員](connection-manager/ole-db-connection-manager.md)|[設定 OLE DB 連線管理員](configure-ole-db-connection-manager.md)|  
    |[SMO 連線管理員](connection-manager/smo-connection-manager.md)|[SMO 連線管理員編輯器](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 連線管理員](connection-manager/smtp-connection-manager.md)|[SMTP 連線管理員編輯器](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 連線管理員](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 連線管理員](connection-manager/wmi-connection-manager.md)|[WMI 連線管理員編輯器](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     您加入的連線管理員將會顯示在方案總管的 [連線管理員] 節點底下。 針對專案中的所有封裝，它也會顯示在 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中。 此索引標籤中連線管理員名稱的前置詞將是 **(專案)**，以區分此專案層級連線管理員以及封裝層級連線管理員。  
  
4.  或者，以滑鼠右鍵按一下方案總管視窗之 [連線管理員] 節點底下的連線管理員 (或) 在 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中，按一下 [重新命名]，然後修改連線管理員的預設名稱。  
  
    > [!NOTE]  
    >  在 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中，您無法覆寫連線管理員名稱中的 **(專案)** 前置詞。 這是原廠設定。  
  
##  <a name="parameter"></a> 若要建立連線管理員屬性的參數  
  
1.  在 [連線管理員] 區域中，以滑鼠右鍵按一下您要建立其參數的連線管理員，然後按一下 [參數化]。  
  
2.  在 [參數化] 對話方塊中設定參數設定。 如需詳細資訊，請參閱[參數化對話方塊](../../2014/integration-services/parameterize-dialog-box.md)。  
  
##  <a name="DeletePackageLevel"></a> 若要從封裝中刪除連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [控制流程] 索引標籤、[資料流程] 索引標籤或 [事件處理常式] 索引標籤，以讓 [連線管理員] 區域可用。  
  
4.  以滑鼠右鍵按一下您要刪除的連線管理員，然後按一下 [刪除]。  
  
     如果您要刪除封裝元素 (如執行 SQL 工作或 OLE DB 來源) 所使用的連線管理員，您將會遇到以下結果：  
  
    -   在封裝元素上出現一個錯誤圖示，表示使用了已刪除的連線管理員。  
  
    -   此封裝驗證失敗。  
  
    -   無法執行此封裝。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
##  <a name="DeleteProjectLevel"></a> 若要刪除共用的連接管理員 （專案層級的連接管理員）  
  
1.  若要刪除專案層級的連線管理員，以滑鼠右鍵按一下方案總管視窗之 [連線管理員] 節點底下的連線管理員，然後按一下 [刪除]。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 會顯示下列警告訊息：  
  
    > [!WARNING]  
    >  刪除專案連接管理員後，使用該連接管理員的封裝可能無法執行。 您無法恢復這個動作。 您要刪除連接管理員嗎?  
  
2.  按一下 [確定] 可刪除該連接管理員，或按一下 [取消] 可保留該連接管理員。  
  
    > [!NOTE]  
    >  您也可以從針對專案中任何封裝開啟之 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中，刪除專案層級的連線管理員。 為此，以滑鼠右鍵按一下索引標籤中的連線管理員，然後按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連線](connection-manager/integration-services-ssis-connections.md)   
 [設定連線管理員的屬性](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
