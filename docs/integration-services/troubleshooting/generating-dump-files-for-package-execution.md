---
title: 產生套件執行的傾印檔案 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1d4761db172138eb86e3cf511b904c5b86b90c4
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65713746"
---
# <a name="generating-dump-files-for-package-execution"></a>產生封裝執行的傾印檔案

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，您可以建立偵錯傾印檔案，以便提供封裝執行的資訊。 這些檔案中的資訊可協助您針對套件執行問題進行疑難排解。  
  
> **注意！** 偵錯傾印檔案可能會包含敏感性資訊。 若要保護敏感性資訊，您可以使用存取控制清單 (ACL) 來限制這些檔案的存取權，或將這些檔案複製到具有存取限制的資料夾。 例如，將偵錯檔案傳送給 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支援服務之前，我們建議您移除任何敏感性或機密資訊。  
  
 當您將某個專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器時，可以建立傾印檔案，這些檔案會提供有關專案中包含之封裝執行的資訊。 當 ISServerExec.exe 程序結束時，會建立傾印檔案。 您可以指定在封裝執行期間發生錯誤時建立傾印檔案，方法是選取 [執行封裝] 對話方塊中的 [在發生錯誤時傾印] 選項。 您也可以使用下列預存程序：  
  
-   [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
     呼叫此預存程序以設定發生任何錯誤或事件時，以及在封裝執行期間發生特定事件時，建立傾印檔案。  
  
-   [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
  
     呼叫此預存程序，使執行中的封裝暫停並建立傾印檔案。  
  
 如果您要使用套件部署模型，請使用 **dtexec** 公用程式或 **dtutil** 公用程式，在命令列指定偵錯傾印選項以建立偵錯傾印檔案。 如需詳細資訊，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)和 [dtutil 公用程式](../../integration-services/dtutil-utility.md)。 如需套件部署模型的詳細資訊，請參閱[部署 Integration Services (SSIS) 專案和套件](https://msdn.microsoft.com/library/hh213290.aspx)和[舊版套件部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)。   
  
## <a name="debug-dump-file-format"></a>偵錯傾印檔案格式  
 當您指定偵錯傾印選項時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 就會建立下列偵錯傾印檔案：  
  
-   .mdmp 偵錯傾印檔案。 這是二進位檔案。  
  
-   .tmp 偵錯傾印檔案。 這是文字格式的檔案。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 預設會將這些檔案儲存至 \<磁碟機>:\Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 資料夾。  
  
 下表僅描述 .tmp 檔案中的特定區段。 .tmp 檔案還包含此表未列出的其他資料。  
  
|資訊類型|Description|範例|  
|-------------------------|-----------------|-------------|  
|環境|作業系統版本、記憶體使用量資料、處理序識別碼及處理序影像名稱。 環境資訊位於 .tmp 檔案的開頭。|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Program Files\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory:58% in use. Physical:845M/2044M  Paging:2404M/4095M (avail/total)|  
|動態連結程式庫 (DLL) 路徑和版本|在處理封裝期間，系統載入之每個 DLL 的路徑和版本號碼。|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module:C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module:C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|最近的訊息|最近系統所發出的訊息。 包括每則訊息的時間、類型、描述和執行緒識別碼。|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Time Stamp:2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID:2368           (ThreadID)<br /><br /> [E:3]         Event Name:OnError                        (EventName)<br /><br /> [E:3]         Source Name:              (SourceName)<br /><br /> [E:3]         Source ID:                      (SourceID)<br /><br /> [E:3]         Execution ID:               (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         Description:元件遺漏、未註冊、無法升級或遺漏必要的介面。 這個元件的連絡資訊是 "__"。|  
  
## <a name="related-information"></a>相關資訊  
 [執行封裝對話方塊](../../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
  
