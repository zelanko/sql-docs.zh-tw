---
title: 設定連線管理員的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], modifying
- modifying connection managers
ms.assetid: 54793114-2198-4d80-8091-e241d5a5d13c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c8581771394ed40f740ea83407b9acd47c6f4ddd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963232"
---
# <a name="set-the-properties-of-a-connection-manager"></a>設定連線管理員的屬性
  所有連接管理員都可以使用 [屬性]**** 視窗進行設定。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 還提供自訂對話方塊，用以修改 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中不同類型的連線管理員。 因連接管理員類型的不同，對話方塊也有不同的選項集。  
  
### <a name="to-modify-a-connection-manager-using-the-properties-window"></a>使用屬性視窗修改連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 SSIS 設計師中，按一下 [控制流程]**** 索引標籤、[資料流程]**** 索引標籤或 [事件處理常式]**** 索引標籤，以讓 [連接管理員]**** 區域可用。  
  
4.  以滑鼠右鍵按一下連接管理員，然後按一下 [屬性]****。  
  
5.  在 [屬性]**** 視窗中編輯屬性值。 針對部分無法在連接管理員之標準編輯器中設定的屬性，[屬性]**** 視窗提供了對這些屬性的存取權。  
  
6.  按一下 [確定]。  
  
7.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>使用連接管理員對話方塊修改連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [控制流程]**** 索引標籤、[資料流程]**** 索引標籤或 [事件處理常式]**** 索引標籤，以讓 [連線管理員]**** 區域可用。  
  
4.  在 [連接管理員]**** 區域中，按兩下連接管理員，以開啟 [連接管理員]**** 對話方塊。 如需有關特定連接管理員類型以及每種類型可用之選項的詳細資訊，請參閱下表。  
  
    |[ODBC 來源編輯器]|選項。|  
    |------------------------|-------------|  
    |[ADO 連線管理員](connection-manager/ado-connection-manager.md)|[設定 OLE DB 連接管理員](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 連線管理員](connection-manager/ado-net-connection-manager.md)|[設定 ADO.NET 連接管理員](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 連線管理員](connection-manager/analysis-services-connection-manager.md)|[加入 Analysis Services 連接管理員對話方塊 UI 參考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 連線管理員](connection-manager/excel-connection-manager.md)|[Excel 連接管理員編輯器](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[檔案連線管理員](connection-manager/file-connection-manager.md)|[檔案連接管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[多重檔案連線管理員](connection-manager/multiple-files-connection-manager.md)|[加入檔案連接管理員對話方塊 UI 參考](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[一般檔案連線管理員](connection-manager/flat-file-connection-manager.md)|[一般檔案連線管理員編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;進階頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[多重一般檔案連線管理員](connection-manager/multiple-flat-files-connection-manager.md)|[多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;進階頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 連線管理員](connection-manager/ftp-connection-manager.md)|[FTP 連線管理員編輯器](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 連線管理員](connection-manager/http-connection-manager.md)|[HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 連線管理員](connection-manager/msmq-connection-manager.md)|[MSMQ 連線管理員編輯器](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 連線管理員](connection-manager/odbc-connection-manager.md)|[ODBC 連接管理員 UI 參考](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 連接管理員](connection-manager/ole-db-connection-manager.md)|[設定 OLE DB 連接管理員](configure-ole-db-connection-manager.md)|  
    |[SMO 連線管理員](connection-manager/smo-connection-manager.md)|[SMO 連線管理員編輯器](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 連線管理員](connection-manager/smtp-connection-manager.md)|[SMTP 連接管理員編輯器](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 連線管理員](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 連線管理員](connection-manager/wmi-connection-manager.md)|[WMI 連線管理員編輯器](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](connection-manager/integration-services-ssis-connections.md)   
 [加入、刪除或共用封裝中的連接管理員](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
  
