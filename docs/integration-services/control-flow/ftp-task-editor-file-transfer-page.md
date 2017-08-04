---
title: "FTP 工作編輯器 （檔案傳輸頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca75f79962fcf7b7cae067a7d841f80f9c4c2032
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="ftp-task-editor-file-transfer-page"></a>FTP 工作編輯器 (檔案傳輸頁面)
  使用 **[FTP 工作編輯器]** 對話方塊的 **[檔案傳輸]** 頁面，來設定工作執行的 FTP 作業。  
  
 若要深入了解此工作，請參閱 [FTP 工作](../../integration-services/control-flow/ftp-task.md)。  
  
## <a name="options"></a>選項。  
 **IsRemotePathVariable**  
 指出遠端路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**True**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 **[RemoteVariable]**。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取此值會顯示動態選項 **[RemotePath]**。|  
  
 **OverwriteFileAtDestination**  
 指定是否可以覆寫目的地端的檔案。  
  
 **IsLocalPathVariable**  
 指出本機路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**True**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 **[LocalVariable]**。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取此值會顯示動態選項 **[LocalPath]**。|  
  
 **運算**  
 選取要執行的 FTP 作業。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**傳送檔案**|傳送檔案。 選取此值會顯示動態選項 **LocalVariable**、 **LocalPathRemoteVariable** 和 **RemotePath**。|  
|**接收檔案**|接收檔案。 選取此值會顯示動態選項 **LocalVariable**、 **LocalPathRemoteVariable** 和 **RemotePath**。|  
|**建立本機目錄**|建立本機目錄。 選取此值會顯示動態選項 **[LocalVariable]** 和 **[LocalPath]**。|  
|**建立遠端目錄**|建立遠端目錄。 選取此值會顯示動態選項 **[RemoteVariable]** 和 **[RemotelPath]**。|  
|**移除本機目錄**|移除本機目錄。 選取此值會顯示動態選項 **[LocalVariable]** 和 **[LocalPath]**。|  
|**移除遠端目錄**|移除遠端目錄。 選取此值會顯示動態選項 **[RemoteVariable]** 和 **[RemotePath]**。|  
|**刪除本機檔案**|刪除本機檔案。 選取此值會顯示動態選項 **[LocalVariable]** 和 **[LocalPath]**。|  
|**刪除遠端檔案**|刪除遠端檔案。 選取此值會顯示動態選項 **[RemoteVariable]** 和 **[RemotePath]**。|  
  
 **IsTransferASCII**  
 指出往返遠端 FTP 伺服器的檔案，是否應以 ASCII 模式傳輸。  
  
## <a name="isremotepathvariable-dynamic-options"></a>IsRemotePathVariable 動態選項  
  
### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **[RemoteVariable]**  
 選取現有的使用者定義變數，或按一下\<**新增變數...**> 以建立使用者定義的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、加入變數  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **[RemotePath]**  
 選取現有的 FTP 連接管理員，或按一下\<**新增連接...**> 若要建立的連接管理員。  
  
 **相關主題**：[FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)、[FTP 連線管理員編輯器](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>IsLocalPathVariable 動態選項  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **[LocalVariable]**  
 選取現有的使用者定義變數，或按一下\<**新增變數...**> 若要建立的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、加入變數  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **[LocalPath]**  
 選取現有的檔案連接管理員，或按一下\<**新增連接...**> 若要建立的連接管理員。  
  
 **相關主題**：[一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)、[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [FTP 工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
  
