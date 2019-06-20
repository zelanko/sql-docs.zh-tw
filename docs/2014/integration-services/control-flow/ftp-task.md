---
title: FTP 工作 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fcc071c10a2daa31190727dfc9f3cbe617bdcb66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831523"
---
# <a name="ftp-task"></a>FTP 工作
  FTP 工作會下載和上傳資料檔以及管理伺服器上的目錄。 例如，封裝可從遠端伺服器或網際網路位置下載資料檔，此工作可視為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝工作流程的一部分。 您可將 FTP 工作用於下列用途：  
  
-   在移動資料之前或之後於目錄之間複製目錄和資料檔，以及將轉換套用至資料。  
  
-   登入來源 FTP 位置並複製檔案或封裝至目的地目錄。  
  
-   從 FTP 位置下載檔案，並在將資料載入資料庫之前，將轉換套用至資料行的資料。  
  
 在執行階段中，FTP 工作會使用 FTP 連接管理員連接到伺服器。 FTP 連接管理員會在 FTP 工作以外另行設定，然後在 FTP 中參考。 FTP 連接管理員包含伺服器設定、存取 FTP 伺服器的認證，以及一些選項如逾時和連接伺服器的重試次數。 如需詳細資訊，請參閱 [FTP Connection Manager](../connection-manager/ftp-connection-manager.md)。  
  
> [!IMPORTANT]  
>  FTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 存取本機檔案或本機目錄時，FTP 工作會使用「檔案」連接管理員或變數中儲存的路徑資訊。 但 FTP 工作存取遠端檔案或遠端目錄時則相反，是使用遠端伺服器上直接指定的路徑 (如 FTP 連接管理員中所指定)，或變數中儲存的路徑資訊。 如需詳細資訊，請參閱[檔案連接管理員](../connection-manager/file-connection-manager.md)和 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)。  
  
 這表示，FTP 工作可接收多個檔案和刪除多個遠端檔案；而如果此工作使用連接管理員，則只能傳送一個檔案且只能刪除一個本機檔案，因為「檔案」連接管理員只能存取一個檔案。 若要存取多個本機檔案，FTP 工作必須使用變數提供路徑資訊。 例如，含有 "C:\Test\\*.txt" 的變數會提供支援刪除或傳送 Test 目錄中所有副檔名為 .txt 的檔案路徑。  
  
 若要傳送多個檔案及存取多個本機檔案和目錄，您也可以將 FTP 工作加入「Foreach 迴圈」中，藉此多次執行 FTP 工作。 「Foreach 迴圈」可使用 For Each File 列舉值，於目錄中跨檔案列舉。 如需詳細資訊，請參閱 [Foreach Loop Container](foreach-loop-container.md)。  
  
 FTP 工作支援在路徑中使用 *?* 及 *\** 萬用字元。 如此即可讓工作存取多個檔案。 不過，您只能在指定檔名的路徑部分使用萬用字元。 例如，C:\MyDirectory\\*.txt 是有效的路徑，而 C:\\\*\MyText.txt 則無效。  
  
 FTP 作業可設定成在作業失敗時停止「檔案系統」工作，或以 ASCII 模式傳送檔案。 傳送和接收檔案副本的作業可設定成覆寫目的地檔案和目錄。  
  
## <a name="predefined-ftp-operations"></a>預先定義的 FTP 作業  
 FTP 工作包括一組預先定義的作業。 下表描述這些作業。  
  
|運算|描述|  
|---------------|-----------------|  
|傳送檔案|從本機電腦將檔案傳送到 FTP 伺服器。|  
|接收檔案|從 FTP 伺服器將檔案儲存到本機電腦。|  
|建立本機目錄|在本機電腦上建立資料夾。|  
|建立遠端目錄|在 FTP 伺服器上建立資料夾。|  
|移除本機目錄|刪除本機電腦上的資料夾。|  
|移除遠端目錄|刪除 FTP 伺服器上的資料夾。|  
|刪除本機檔案|刪除本機電腦上的檔案。|  
|刪除遠端檔案|刪除 FTP 伺服器上的檔案。|  
  
## <a name="custom-log-entries-available-on-the-ftp-task"></a>FTP 工作上可用的自訂記錄項目  
 下表列出 FTP 工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`FTPConnectingToServer`|指出工作已經起始與 FTP 伺服器的連接。|  
|`FTPOperation`|報告工作執行之 FTP 作業的開始及其類型。|  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具中設定這些屬性的詳細資訊，請參閱 [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)。  
  
 如需以程式設計方式設定這些屬性的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>。  
  
## <a name="see-also"></a>另請參閱  
 [FTP 工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)   
 [FTP 工作編輯器 &#40;檔案傳輸頁面&#41;](../ftp-task-editor-file-transfer-page.md)   
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
