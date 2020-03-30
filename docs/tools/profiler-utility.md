---
title: Profiler 公用程式
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], profiler90 utility
- profiler90 utility
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: e91c30a9-0d29-4f84-bcb8-e8fb62afadda
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ed207e5fa854dc25a07edfff49a75aad9d370ff
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307390"
---
# <a name="profiler-utility"></a>Profiler 公用程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
 **/U** *login_id*  
 這是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證的使用者登入識別碼。 登入識別碼會區分大小寫。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]第 1 課：建立 Windows Azure 儲存體物件{2}。  
  
 **/P** *password*  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證之使用者指定的密碼。  
  
 **/E**  
 利用目前使用者的認證來指定以 Windows 驗證進行連接。  
  
 **/S**  *sql_server_name*  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。 Profiler 會利用 **/U** 和 **/P** 參數或 **/E** 參數所指定的驗證資訊，自動連接指定的伺服器。 若要連線到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的具名執行個體，請使用 **/S** *sql_server_name*\\*instance_name*。  
  
 **/A**  *analysis_services_server_name*  
 指定 Analysis Services 的執行個體。 Profiler 會利用 **/U** 和 **/P** 參數或 **/E** 參數所指定的驗證資訊，自動連接指定的伺服器。 若要連線到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的具名執行個體，請使用 **/A** *analysis_services_server_name\instance_name*。  
  
 **/D** *database*  
 指定連接要用的資料庫名稱。 如果未指定任何資料庫，這個選項會選取指定使用者的預設資料庫。  
  
 **/B "** *trace_table_name* **"**  
 指定啟動 Profiler 時所載入的追蹤資料表。 您必須指定資料庫、使用者或結構描述，以及資料表。  
  
 **/T"** *template_name* **"**  
 指定將載入來設定追蹤的範本。 範本名稱必須用引號括住。 範本名稱必須在系統範本目錄中，或在使用者範本目錄中。 如果兩個目錄中有同名的兩個範本存在，就會載入系統目錄中的範本。 如果沒有含指定名稱的範本，便會載入標準範本。 請注意，在 <範本名稱>  中，不應指定範本的副檔名 (.tdf)。 例如：  
  
```  
/T "standard"  
```  
  
 **/F"** *filename* **"**  
 指定啟動 Profiler 時所載入之追蹤檔的路徑和檔案名稱。 整個路徑和檔案名稱必須用引號括住。 這個選項不能搭配 **/O**一起使用。  
  
 **/O "** *filename*  **"**  
 指定應該寫入追蹤結果之檔案的路徑和檔案名稱。 整個路徑和檔案名稱必須用引號括住。 這個選項不能搭配 **/F**一起使用。  
  
 **/L** *locale_ID*  
 無法使用。  
  
 **/M "** *MM-DD-YY hh:mm:ss* **"**  
 指定停止追蹤的日期和時間。 停止時間必須用引號括住。 請根據下表中的參數來指定停止時間：  
  
|參數|定義|  
|---------------|----------------|  
|MM|兩位數的月份|  
|DD|兩位數的日期|  
|YY|兩位數的年份|  
|hh|兩位數的小時 (24 小時制)|  
|mm|兩位數的分鐘|  
|ss|兩位數的秒鐘|  
  
> [!NOTE]  
>  只有當  **中已啟用 [使用地區設定顯示日期與時間值]** [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 選項時，才能使用 "MM-DD-YY hh:mm:ss" 格式。 如果這個選項未啟用，您必須使用 "YYYY-MM-DD hh:mm:ss" 日期和時間格式。  
  
 **/R**  
 啟用追蹤檔的換用。  
  
 **/Z**  *file_size*  
 指定追蹤檔的大小 (以 MB 為單位)。 預設大小是 5 MB。 如果啟用換用，所有換用檔案都不能超出這個引數所指定的值。  
  
## <a name="remarks"></a>備註  
 若要利用特定範本啟動追蹤，請同時使用 **/S** 和 **/T** 選項。 例如，若要利用 MyServer\MyInstance 上的 Standard 範本啟動追蹤，請在命令提示字元之下輸入下列命令：  
  
```  
profiler /S MyServer\MyInstance /T "Standard"  
```  
  
## <a name="see-also"></a>另請參閱  
 [命令提示字元公用程式參考 &#40;Database Engine&#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
