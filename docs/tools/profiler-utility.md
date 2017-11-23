---
title: "Profiler 公用程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command prompt utilities [SQL Server], profiler90 utility
- profiler90 utility
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: e91c30a9-0d29-4f84-bcb8-e8fb62afadda
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 441d4cdd25e2c0c9db0a6d9a1d6a1704a0d474b3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="profiler-utility"></a>Profiler 公用程式
  **profiler** 公用程式會啟動 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 工具。 這個主題稍後列出的選擇性引數可讓您控制應用程式啟動的方式。  
  
> [!NOTE]  
>  **profiler** 公用程式的用途不在於編寫追蹤的指令碼。 如需詳細資訊，請參閱 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
profiler  
    [ /? ] |  
[  
{  
{ /U login_id [ /P password ] }  
| /E  
}  
{[ /S sql_server_name ] | [ /A analysis_services_server_name ] }  
[ /D database ]  
[ /T "template_name" ]  
[ /B { "trace_table_name" } ]  
{ [/F "filename" ] | [ /O "filename" ] }  
[ /L locale_ID ]  
[ /M "MM-DD-YY hh:mm:ss" ]  
[ /R ]  
[ /Z file_size ]  
]  
```  
  
## <a name="arguments"></a>引數  
 **/?**  
 顯示 **profiler** 引數的語法摘要。  
  
 **/U** <登入識別碼>  
 這是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證的使用者登入識別碼。 登入識別碼會區分大小寫。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]。  
  
 **/P** <密碼>  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證之使用者指定的密碼。  
  
 **/E**  
 利用目前使用者的認證來指定以 Windows 驗證進行連接。  
  
 **/S** <SQL Server 名稱>  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。 Profiler 會利用 **/U** 和 **/P** 參數或 **/E** 參數所指定的驗證資訊，自動連接指定的伺服器。 若要連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的具名執行個體，請使用 **/S** <SQL Server 名稱>\\<執行個體名稱>。  
  
 **/A** <Analysis Services 伺服器名稱>  
 指定 Analysis Services 的執行個體。 Profiler 會利用 **/U** 和 **/P** 參數或 **/E** 參數所指定的驗證資訊，自動連接指定的伺服器。 若要連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的具名執行個體，請使用 **/A** <Analysis Services 伺服器名稱>\<執行個體名稱> 的格式。  
  
 **/D** <資料庫>  
 指定連接要用的資料庫名稱。 如果未指定任何資料庫，這個選項會選取指定使用者的預設資料庫。  
  
 **/B "** <追蹤資料表名稱> **"**  
 指定啟動 Profiler 時所載入的追蹤資料表。 您必須指定資料庫、使用者或結構描述，以及資料表。  
  
 **/T "** <範本名稱> **"**  
 指定將載入來設定追蹤的範本。 範本名稱必須用引號括住。 範本名稱必須在系統範本目錄中，或在使用者範本目錄中。 如果兩個目錄中有同名的兩個範本存在，就會載入系統目錄中的範本。 如果沒有含指定名稱的範本，便會載入標準範本。 請注意，在 <範本名稱> 中，不應指定範本的副檔名 (.tdf)。 例如：  
  
```  
/T "standard"  
```  
  
 **/F "** <檔案名稱> **"**  
 指定啟動 Profiler 時所載入之追蹤檔的路徑和檔案名稱。 整個路徑和檔案名稱必須用引號括住。 這個選項不能搭配 **/O** 一起使用。  
  
 **/O "** <檔案名稱> **"**  
 指定應該寫入追蹤結果之檔案的路徑和檔案名稱。 整個路徑和檔案名稱必須用引號括住。 這個選項不能搭配 **/F** 一起使用。  
  
 **/L** <地區設定識別碼>  
 無法使用。  
  
 **/M "** *MM-DD-YY hh:mm:ss* **"**  
 指定停止追蹤的日期和時間。 停止時間必須用引號括住。 請根據下表中的參數來指定停止時間：  
  
|參數|定義|  
|---------------|----------------|  
|MM|兩位數的月份|  
|DD|兩位數的日期|  
|YY|兩位數的年份|  
|hh|兩位數的小時 (24 小時制)|  
|MM|兩位數的分鐘|  
|ss|兩位數的秒鐘|  
  
> [!NOTE]  
>  只有當 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 中已啟用 [使用地區設定顯示日期與時間值] 選項時，才能使用 "MM-DD-YY hh:mm:ss" 格式。 如果這個選項未啟用，您必須使用 "YYYY-MM-DD hh:mm:ss" 日期和時間格式。  
  
 **/R**  
 啟用追蹤檔的換用。  
  
 **/Z** <檔案大小>  
 指定追蹤檔的大小 (以 MB 為單位)。 預設大小是 5 MB。 如果啟用換用，所有換用檔案都不能超出這個引數所指定的值。  
  
## <a name="remarks"></a>備註  
 若要利用特定範本啟動追蹤，請同時使用 **/S** 和 **/T** 選項。 例如，若要利用 MyServer\MyInstance 上的 Standard 範本啟動追蹤，請在命令提示字元之下輸入下列命令：  
  
```  
profiler /S MyServer\MyInstance /T "Standard"  
```  
  
## <a name="see-also"></a>另請參閱  
 [命令提示字元公用程式參考 &#40;Database Engine&#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
