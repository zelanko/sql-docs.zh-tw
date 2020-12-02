---
description: FTP 工作
title: FTP 工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftptask.f1
- sql13.dts.designer.ftptask.general.f1
- sql13.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 013fffc66c8e40ca2124b949f555e0638df7967e
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127399"
---
# <a name="ftp-task"></a>FTP 工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  FTP 工作會下載和上傳資料檔以及管理伺服器上的目錄。 例如，封裝可從遠端伺服器或網際網路位置下載資料檔，此工作可視為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝工作流程的一部分。 您可將 FTP 工作用於下列用途：  
  
-   在移動資料之前或之後於目錄之間複製目錄和資料檔，以及將轉換套用至資料。  
  
-   登入來源 FTP 位置並複製檔案或封裝至目的地目錄。  
  
-   從 FTP 位置下載檔案，並在將資料載入資料庫之前，將轉換套用至資料行的資料。  
  
 在執行階段中，FTP 工作會使用 FTP 連接管理員連接到伺服器。 FTP 連接管理員會在 FTP 工作以外另行設定，然後在 FTP 中參考。 FTP 連接管理員包含伺服器設定、存取 FTP 伺服器的認證，以及一些選項如逾時和連接伺服器的重試次數。 如需詳細資訊，請參閱 [FTP Connection Manager](../../integration-services/connection-manager/ftp-connection-manager.md)。  
  
> [!IMPORTANT]  
>  FTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 存取本機檔案或本機目錄時，FTP 工作會使用「檔案」連接管理員或變數中儲存的路徑資訊。 但 FTP 工作存取遠端檔案或遠端目錄時則相反，是使用遠端伺服器上直接指定的路徑 (如 FTP 連接管理員中所指定)，或變數中儲存的路徑資訊。 如需詳細資訊，請參閱[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)和 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  
  
 這表示，FTP 工作可接收多個檔案和刪除多個遠端檔案；而如果此工作使用連接管理員，則只能傳送一個檔案且只能刪除一個本機檔案，因為「檔案」連接管理員只能存取一個檔案。 若要存取多個本機檔案，FTP 工作必須使用變數提供路徑資訊。 例如，變數如果含有 "C:\Test\&#42;.txt"，其提供的路徑便可支援刪除或傳送 [Test] 目錄中所有副檔名為 .txt 的檔案。  
  
 若要傳送多個檔案及存取多個本機檔案和目錄，您也可以將 FTP 工作加入「Foreach 迴圈」中，藉此多次執行 FTP 工作。 「Foreach 迴圈」可使用 For Each File 列舉值，於目錄中跨檔案列舉。 如需詳細資訊，請參閱 [Foreach 迴圈容器](../../integration-services/control-flow/foreach-loop-container.md)＞。  
  
 FTP 工作支援在路徑中使用 *?* 及 *\** 萬用字元。 如此即可讓工作存取多個檔案。 不過，您只能在指定檔名的路徑部分使用萬用字元。 例如，C:\MyDirectory\\*.txt 是有效的路徑，而 C:\\\*\MyText.txt 則無效。  
  
 FTP 作業可設定成在作業失敗時停止「檔案系統」工作，或以 ASCII 模式傳送檔案。 傳送和接收檔案副本的作業可設定成覆寫目的地檔案和目錄。  
  
## <a name="predefined-ftp-operations"></a>預先定義的 FTP 作業  
 FTP 工作包括一組預先定義的作業。 下表描述這些作業。  
  
|作業|描述|  
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
 下表列出 FTP 工作的自訂記錄項目。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|**FTPConnectingToServer**|指出工作已經起始與 FTP 伺服器的連接。|  
|**FTPOperation**|報告工作執行之 FTP 作業的開始及其類型。|  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具中設定這些屬性的詳細資訊，請參閱 [設定工作或容器的屬性](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
 如需以程式設計方式設定這些屬性的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>。  
  
## <a name="ftp-task-editor-general-page"></a>FTP 工作編輯器 (一般頁面)
  使用 **[FTP 工作編輯器]** 對話方塊的 **[一般]** 頁面，即可指定 FTP 連接管理員，以連接到工作進行通訊的 FTP 伺服器。 您也可以命名和描述 FTP 工作。  
  
### <a name="options"></a>選項。  
 **FtpConnection**  
 選取現有的 FTP 連線管理員，或按一下 \<**New connection...**> 來建立連線管理員。  
  
> [!IMPORTANT]  
>  FTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 **相關主題**：[FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)、[FTP 連線管理員編輯器](../connection-manager/ftp-connection-manager.md)  
  
 **StopOnFailure**  
 指出當 FTP 作業失敗時，FTP 工作是否結束。  
  
 **名稱**  
 為 FTP 工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入 FTP 工作的描述。  
  
## <a name="ftp-task-editor-file-transfer-page"></a>FTP 工作編輯器 (檔案傳輸頁面)
  使用 **[FTP 工作編輯器]** 對話方塊的 **[檔案傳輸]** 頁面，來設定工作執行的 FTP 作業。  
  
### <a name="options"></a>選項。  
 **IsRemotePathVariable**  
 指出遠端路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**True**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 **[RemoteVariable]** 。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取此值會顯示動態選項 **[RemotePath]** 。|  
  
 **OverwriteFileAtDestination**  
 指定是否可以覆寫目的地端的檔案。  
  
 **IsLocalPathVariable**  
 指出本機路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**True**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 **[LocalVariable]** 。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取此值會顯示動態選項 **[LocalPath]** 。|  
  
 **運算**  
 選取要執行的 FTP 作業。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**傳送檔案**|傳送檔案。 選取此值會顯示動態選項 **LocalVariable**、 **LocalPathRemoteVariable** 和 **RemotePath**。|  
|**接收檔案**|接收檔案。 選取此值會顯示動態選項 **LocalVariable**、 **LocalPathRemoteVariable** 和 **RemotePath**。|  
|**建立本機目錄**|建立本機目錄。 選取此值會顯示動態選項 **[LocalVariable]** 和 **[LocalPath]** 。|  
|**建立遠端目錄**|建立遠端目錄。 選取此值會顯示動態選項 **[RemoteVariable]** 和 **[RemotelPath]** 。|  
|**移除本機目錄**|移除本機目錄。 選取此值會顯示動態選項 **[LocalVariable]** 和 **[LocalPath]** 。|  
|**移除遠端目錄**|移除遠端目錄。 選取此值會顯示動態選項 **[RemoteVariable]** 和 **[RemotePath]** 。|  
|**刪除本機檔案**|刪除本機檔案。 選取此值會顯示動態選項 **[LocalVariable]** 和 **[LocalPath]** 。|  
|**刪除遠端檔案**|刪除遠端檔案。 選取此值會顯示動態選項 **[RemoteVariable]** 和 **[RemotePath]** 。|  
  
 **IsTransferASCII**  
 指出往返遠端 FTP 伺服器的檔案，是否應以 ASCII 模式傳輸。  
  
### <a name="isremotepathvariable-dynamic-options"></a>IsRemotePathVariable 動態選項  
  
#### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **[RemoteVariable]**  
 選取現有的使用者定義變數，或按一下 \<**New variable...**> 來建立使用者定義變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、新增變數  
  
#### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **[RemotePath]**  
 選取現有的 FTP 連線管理員，或按一下 \<**New connection...**> 來建立連線管理員。  
  
 **相關主題：** [FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)、[FTP 連線管理員編輯器](../connection-manager/ftp-connection-manager.md)  
  
### <a name="islocalpathvariable-dynamic-options"></a>IsLocalPathVariable 動態選項  
  
#### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **[LocalVariable]**  
 選取現有的使用者定義變數，或按一下 \<**New variable...**> 來建立變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、新增變數  
  
#### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **[LocalPath]**  
 選取現有的檔案連線管理員，或按一下 \<**New connection...**> 來建立連線管理員。  
  
 **相關主題**：[一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
