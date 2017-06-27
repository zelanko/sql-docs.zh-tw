---
title: "SSMS 公用程式 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 6dccaff93a6c8b2374a1fad069b2f597898802fc
ms.openlocfilehash: 84b9b39b9a7ae03244dd3703cc303d1cf7f4380b
ms.contentlocale: zh-tw
ms.lasthandoff: 06/23/2017

---
# <a name="ssms-utility"></a>Ssms 公用程式
  **Ssms** 公用程式會開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 如果有指定， **Ssms** 也會建立伺服器的連接，且會開啟查詢、指令碼、檔案、專案和方案。  
  
 您可以指定包含查詢、專案或方案的檔案。 如果提供了連接資訊，且檔案類型與這個類型的伺服器相關聯，包含查詢的檔案會自動連接伺服器。 例如，.sql 檔會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中開啟一個 [SQL 查詢編輯器] 視窗，.mdx 檔會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中開啟一個 [MDX 查詢編輯器] 視窗。 而**SQL Server 方案和專案** 會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中開啟。  
  
> [!NOTE]  
>  **Ssms** 公用程式不會執行查詢。 若要從命令列中執行查詢，請使用 **sqlcmd** 公用程式。  
  
## <a name="syntax"></a>語法  
  
```  
  
Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-S servername] [-d databasename] [-U username] [-P password]   
    [-E] [-nosplash] [-log [filename]?] [-?]  
```  
  
## <a name="arguments"></a>引數  
 *scriptfile*  
 指定一個或多個要開啟的指令碼檔案。 這個參數必須包含檔案的完整路徑。  
  
 *projectfile*  
 指定要開啟的指令碼專案。 這個參數必須包含指令碼專案檔的完整路徑。  
  
 *solutionfile*  
 指定要開啟的方案。 這個參數必須包含方案檔的完整路徑。  
  
 [**-S** *servername*]  
 伺服器名稱  
  
 [**-d** *databasename*]  
 資料庫名稱  
  
 [**-U** *username*]  
 利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來連接時的使用者名稱  
  
 [**-P** *password*]  
 利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來連接時的密碼  
  
 [**-E**]  
 使用 Windows 驗證進行連接  
  
 [**-nosplash**]  
 在開啟時，使 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 不呈現開頭顯示畫面。 當您利用頻寬有限的連接，透過「終端機服務」來連接執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的電腦時，請使用這個選項。 這個引數不區分大小寫，可出現在其他引數的前後。  
  
 [**-log***[filename]?*]  
 將 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 活動記錄到指定的檔案以利於進行疑難排解  
  
 [**-?**]  
 顯示命令列說明  
  
## <a name="remarks"></a>備註  
 所有參數都是選擇性的，除了用逗號來分隔的檔案之外，您必須用空格來分隔它們。 如果您沒有指定任何參數，**Ssms** 會依照 [工具] 功能表上，[選項] 設定中所指定的內容來開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 例如，如果 [環境/一般] 頁面的 [啟動時] 選項指定 [開啟新增查詢視窗]，**Ssms** 會以空白的查詢編輯器開啟。  
  
 **-log** 參數必須出現在命令列結尾，位於所有其他參數之後。 檔名引數是選擇性的。 如果指定了檔名，但該檔案不存在，便會建立檔案。 若因寫入權限不足等緣故而無法建立檔案，則會改將記錄寫入未當地語系化的 APPDATA 位置 (請參閱下文)。 如果未指定檔名引數，便會將兩個檔案寫入至目前使用者的未當地語系化應用程式儲存資料夾。 SQL Server 的未當地語系化應用程式儲存資料夾可以由 APPDATA 環境變數查知。 例如，SQL Server 2012 的資料夾是 \<系統磁碟機>:\Users\\<使用者名稱\>\AppData\Roaming\Microsoft\AppEnv\10.0\\。 兩個檔案依預設將名為 ActivityLog.xml 和 ActivityLog.xsl。 前者包含活動記錄資料，後者則是 XML 樣式表以讓您更方便檢視此 XML 檔案。 請使用下列步驟，在您的預設 XML 檢視器 (如 Internet Explorer) 中檢視記錄檔：按一下 [開始]，再按一下 [執行]，然後在提供的欄位內鍵入「\<系統磁碟機>:\Users\\<使用者名稱\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml」，然後按 Enter 鍵。  
  
 如果提供了連接資訊，且檔案類型與這個類型的伺服器相關聯，便會發出包含查詢的檔案連接到伺服器的提示。 例如，.sql 檔會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中開啟一個 [SQL 查詢編輯器] 視窗，.mdx 檔會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中開啟一個 [MDX 查詢編輯器] 視窗。 而**SQL Server 方案和專案** 會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中開啟。  
  
 下表將伺服器類型對應至副檔名。  
  
|伺服器類型|延伸模組|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|  
|SQL Server Analysis Services|.mdx<br /><br /> .xmla|  
  
## <a name="examples"></a>範例  
 下列指令碼會在命令提示字元之下，利用預設值來開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ：  
  
```  
Ssms  
  
```  
  
 下列指令碼會在命令提示字元之下，將程式碼編輯器設為伺服器 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，在不呈現開頭顯示畫面的情況下，利用 Windows 驗證來開啟 `ACCTG and the database AdventureWorks2012,` ：  
  
```  
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash  
  
```  
  
 下列指令碼會在命令提示字元之下開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，且會開啟 MonthEndQuery 指令碼。  
  
```  
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"  
  
```  
  
 下列指令碼會在命令提示字元之下開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，且會在名稱為 `developer`的電腦上開啟 NewReportsProject 專案：  
  
```  
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"  
  
```  
  
 下列指令碼會在命令提示字元之下開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，且會開啟 MonthlyReports 方案：  
  
```  
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
  
  
