---
title: RS.exe 公用程式 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- automatic report server tasks
- rs utility
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], automating tasks
- command prompt utilities [SQL Server], rs
- scripts [Reporting Services], command prompt
- deploying reports [Reporting Services]
ms.assetid: bd6f958f-cce6-4e79-8a0f-9475da2919ce
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0ebd18967f892d0f40e5d5b0e3b15e1196935af8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141838"
---
# <a name="rsexe-utility-ssrs"></a>RS.exe Utility (SSRS)
  rs.exe 公用程式會處理您在輸入檔中所提供的指令碼。 使用此公用程式可自動化報表伺服器部署和管理工作。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，可支援 **rs** 公用程式，運作於設定 SharePoint 整合模式的報表伺服器以及以原生模式設定的伺服器中。 之前舊版只支援原生模式設定。  
  
 **本主題內容：**  
  
-   [檔案位置](#bkmk_filelocation)  
  
-   [引數](#bkmk_arguments)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [範例](#bkmk_examples)  
  
## <a name="syntax"></a>語法  
  
```  
  
      rs {-?}  
{-i input_file=}  
{-s serverURL}  
{-u username}  
{-p password}  
{-e endpoint}  
{-l time_out}  
{-b batchmode}  
{-v globalvars=}  
{-t trace}  
```  
  
##  <a name="bkmk_filelocation"></a> 檔案位置  
 **RS.exe** 位在 **\Program Files\Microsoft SQL Server\110\Tools\Binn**。 您可以從檔案系統上的任何資料夾執行此公用程式。  
  
##  <a name="bkmk_arguments"></a> 引數  
 **-?**  
 (選擇性) 顯示 **rs** 引數的語法。  
  
 `-i` *輸入檔案*  
 (必要) 指定要執行的 .rss 檔案。 這個值可以是 .rss 檔案的相對路徑或完整路徑。  
  
 `-s` *serverURL*  
 (必要) 指定要對其執行檔案的 Web 伺服器名稱和報表伺服器虛擬目錄名稱。 報表伺服器 URL 的範例為 `http://examplewebserver/reportserver`。 伺服器名稱開頭的前置詞 http:// 或 https:// 是選擇性的。 如果您省略前置詞，報表伺服器 Script Host 會先嘗試使用 https，而且如果 https 無法運作，則會使用 http。  
  
 `-u` [*網域*\\]*使用者名稱*  
 (選擇性) 指定用來連接到報表伺服器的使用者帳戶。 如果省略 `-u` 和 `-p`，則會使用目前的 Windows 使用者帳戶。  
  
 `-p` *密碼*  
 (需要`-u`指定) 指定要搭配使用的密碼`-u`引數。 此值區分大小寫。  
  
 `-e`  
 (選擇性) 指定要在其上執行指令碼的 SOAP 結束點。 有效的值如下：  
  
-   Mgmt2010  
  
-   Mgmt2006  
  
-   Mgmt2005  
  
-   Exec2005  
  
 如果未指定值，則會使用 Mgmt2005 端點。 如需有關 SOAP 端點的詳細資訊，請參閱 <<c0> [ 報表伺服器 Web 服務端點](../report-server-web-service/methods/report-server-web-service-endpoints.md)。  
  
 `-l` *time_out*  
 (選擇性) 指定與伺服器的連接逾時之前所經過的秒數。預設值是 60 秒。 若未指定逾時值，則使用預設值。 `0` 的值指定連接永不逾時。  
  
 **-b**  
 (選擇性) 指定以批次方式執行指令碼檔案中的命令。 若有任何命令失敗，便會回復此批次。 有些命令無法批次處理，而會依平常方式執行。 只有在指令碼中發生未處理的例外狀況會導致批次復原。 如果指令碼處理例外狀況，並從正常地傳回`Main`，會認可該批次。 如果忽略此參數，則會執行此命令而不會建立批次。 如需詳細資訊，請參閱 < [Batching Methods](../report-server-web-service-net-framework-soap-headers/batching-methods.md)。  
  
 `-v` *globalvar*  
 (選擇性) 指定在指令碼中使用的全域變數。 如果指令碼使用全域變數，則必須指定此引數。 指定的值必須是 .rss 檔案中所定義的全域變數之有效值。 您必須為每個 **–v** 引數指定一個全域變數。  
  
 會在命令列上指定 `-v` 引數，以及用於設定在執行階段定義於指令碼中的全域變數值。 例如，如果您的指令碼包含名為 *parentFolder*的變數，您就可以在命令列上指定該資料夾的名稱：  
  
 `rs.exe -i myScriptFile.rss -s http://myServer/reportserver -v parentFolder="Financial Reports"`  
  
 全域變數會使用給定的名稱來建立並設定為所提供的值。 比方說， **-v =**"`1`" **-v b =**」`2`"會產生名為的變數`a`值為"`1`"和變數**b**值為"`2`」。  
  
 指令碼中的任何函數均可使用全域變數。 反斜線和引號 (**\\"**) 將被解譯為雙引號。 只有當字串含有空格時才需要引號。 變數名稱必須是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]的有效名稱。它們必須以字母字元或底線符號為開頭，而且包含字母字元、數字或底線符號。 保留字不可以當做變數名稱使用。 如需使用全域變數的詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
 **-t**  
 (選擇性) 追蹤記錄的輸出錯誤訊息。 此引數沒有取得值。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)。  
  
##  <a name="bkmk_permissions"></a> 權限  
 若要執行工具，您必須有足夠的權限，可以連接到要對其執行指令碼的報表伺服器執行個體。 您可以執行指令碼在本機電腦或遠端電腦執行變更。 若要對安裝在遠端電腦上的報表伺服器執行變更，請在 `-s` 引數中指定遠端電腦。  
  
##  <a name="bkmk_examples"></a> 範例  
 下列範例說明如何指定指令碼檔案，其中包含您要執行的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 指令碼和 Web 服務方法。  
  
```  
rs –i c:\scriptfiles\script_copycontent.rss -s http://localhost/reportserver  
```  
  
 如需詳細的範例，請參閱＜ [在報表伺服器之間移轉內容的範例 Reporting Services rs.exe 指令碼](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。  
  
 如需其他範例，請參閱[執行 Reporting Services 指令碼檔案](run-a-reporting-services-script-file.md)  
  
## <a name="remarks"></a>備註  
 您可以定義指令碼來設定系統屬性、發行報表等等。 您可以建立的指令碼包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API 的任何方法。 如需有關的方法和屬性可供您的詳細資訊，請參閱[報表伺服器 Web 服務](../report-server-web-service/report-server-web-service.md)。  
  
 指令碼必須以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 程式碼撰寫，然後使用 .rss 副檔名將指令碼儲存在 Unicode 或 UTF-8 文字檔中。 您不可以使用 **rs** 公用程式來偵錯指令碼。 若要偵錯指令碼，請在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]中執行該程式碼。  
  
> [!TIP]  
>  如需詳細的範例，請參閱＜ [在報表伺服器之間移轉內容的範例 Reporting Services rs.exe 指令碼](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [執行 Reporting Services 指令碼檔案](run-a-reporting-services-script-file.md)   
 [編寫部署和管理工作的指令碼](script-deployment-and-administrative-tasks.md)   
 [利用 rs.exe 公用程式和 Web 服務編寫指令碼](script-with-the-rs-exe-utility-and-the-web-service.md)   
 [報表伺服器命令提示字元公用程式&#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)  
  
  
