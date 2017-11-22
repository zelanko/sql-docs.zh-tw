---
title: "sqlservr 應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbf4124c957394d692976eef60d62742741bd949
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="sqlservr-application"></a>sqlservr 應用程式
  **sqlservr** 應用程式會在命令提示字元之下，啟動、停止、暫停和繼續執行 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlservr [-sinstance_name] [-c] [-dmaster_path] [-f]   
     [-eerror_log_path] [-lmaster_log_path] [-m]  
     [-n] [-Ttrace#] [-v] [-x] [-gnumber]  
```  
  
## <a name="arguments"></a>引數  
 **-s** *instance_name*  
 指定要連接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。 如果未指定任何具名執行個體， **sqlservr** 會啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的預設執行個體。  
  
> [!IMPORTANT]  
>  啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體時，您必須使用該執行個體之適當目錄中的 **sqlservr** 應用程式。 如果是預設的執行個體，請執行 \MSSQL\Binn 目錄中的 **sqlservr** 。 如果是具名執行個體，請執行 \MSSQL$ **instance_name** \Binn 目錄中的*sqlservr*。  
  
 **-c**  
 指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體會於 Windows 服務控制管理員之外個別啟動。 當在命令提示字元之下啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 時，這個選項可用來縮短啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所花的時間。  
  
> [!NOTE]  
>  使用此選項時，您不可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務管理員或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] net stop **命令停止** ，而且如果您登出該電腦， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 也會停止。  
  
 **-d** *master_path*  
 指出 **master** 資料庫檔案的完整路徑。 **-d** 和 *master_path*之間沒有空格。 如果不提供這個選項，會使用現有的登錄參數。  
  
 **-f**  
 啟動只含最小組態的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。 如果組態值設定 (如過度調配記憶體) 造成伺服器無法啟動，這就很有用。  
  
 **-e** *error_log_path*  
 指出錯誤記錄檔的完整路徑。 如果未指定，預設位置是*\<磁碟機 >*: \Program Files\Microsoft SQL Server\MSSQL\Log\Errorlog 預設執行個體和*\<磁碟機 >*: \Program Files\Microsoft SQL Server\MSSQL$*instance_name*\Log\Errorlog 具名執行個體。 **-e** 和 *error_log_path*之間沒有空格。  
  
 **-l** *master_log_path*  
 指出 **master** 資料庫交易記錄檔的完整路徑。 **-l** 和 *master_log_path*之間沒有空格。  
  
 **-m**  
 指出要啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的單一使用者模式。 啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的單一使用者模式時，只能連接單一使用者。 不會啟動「保證從磁碟快取中，將已完成的交易定期寫入資料庫裝置」的 CHECKPOINT 機制。 (一般而言，如果系統資料庫發生需要修復的問題，便會使用這個選項。)這個選項會啟用 **sp_configure allow updates** 選項。 預設會停用 **allow updates** 。  
  
 **-n**  
 可讓您啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的具名執行個體。 如果沒有設定 **-s** 參數，就會嘗試啟動預設執行個體。 您必須先在命令提示字元處切換至該執行個體的適當 BINN 目錄，才能啟動 **sqlservr.exe**。 例如，如果 Instance1 原先為二進位編碼檔案使用 \mssql$Instance1，使用者就必須位於 \mssql$Instance1\binn 目錄中，才能啟動 **sqlservr.exe -s instance1**。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -n **-n** 的執行個體，建議您也要使用 **-e** 選項，否則不會記錄 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 事件。  
  
 **-T** *trace#*  
 指出啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，應該已啟用指定的追蹤旗標 (*trace#*)。 追蹤旗標用來啟動具有非標準行為的伺服器。 如需詳細資訊，請參閱[追蹤旗標&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
> [!IMPORTANT]  
>  指定追蹤旗標時，請使用 **-T** 傳遞追蹤旗標號碼。 **接受小寫的 t (**-t [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])；但是 **-t** 是用來設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援工程師所需要的其他內部追蹤旗標。  
  
 **-v**  
 顯示伺服器版本號碼。  
  
 **-x**  
 停止保留 CPU 時間和快取命中率統計資料。 允許最大效能。  
  
 **-g** *memory_to_reserve*  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 保留給在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 處理序之內但在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 記憶體集區之外的記憶體配置，所能使用的記憶體整數數量 (MB)。 記憶體集區外的記憶體，是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用來載入項目的區域，例如擴充程序 `.dll` 檔、分散式查詢參考的 OLE DB 提供者，以及 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式所參考的自動化物件。 預設值為 256 MB。  
  
 使用這個選項可能有助於微調記憶體配置，不過，實體記憶體必須已超出作業系統在應用程式能夠使用的虛擬記憶體上所設定的限制。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的記憶體使用需求不合規則且 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 處理序的虛擬位址空間全部都在使用的大型記憶體組態中，可能適合使用這個選項。 使用此選項不正確時，可能會造成無法啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的狀況，也可能會發生執行階段錯誤。  
  
 除非您在 **錯誤記錄檔中見到下列任何警告，否則，請使用** -g [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 參數的預設值：  
  
-   "Failed Virtual Allocate Bytes: FAIL_VIRTUAL_RESERVE \<大小>"  
  
-   "Failed Virtual Allocate Bytes: FAIL_VIRTUAL_COMMIT \<大小>"  
  
 這些訊息可能表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 正在嘗試釋出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 記憶體集區的可用部分，以便找出擴充預存程序 .dll 檔或自動化物件等項目的空間。 在這種情況下，可考慮加大 **-g**`` 參數所保留的記憶體數量。  
  
 使用低於預設值的值，會增加緩衝集區和執行緒堆疊所能使用的記憶體數量，且可能在並未使用許多擴充預存程序、分散式查詢或自動化物件的系統中，使需要大量記憶體的工作負載因而提升效能。  
  
## <a name="remarks"></a>備註  
 在大部分情況下，sqlservr.exe 程式只用來進行疑難排解或主要的維護工作。 在命令提示字元處利用 sqlservr.exe 啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不會以服務形式啟動，因此，您無法使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] net **命令停止** 。 使用者可以連接至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，但 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具會顯示該服務的狀態， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員因而可正確地指出該服務已經停止。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可以連接到伺服器，但它也會指出該服務已經停止。  
  
## <a name="compatibility-support"></a>相容性支援  
 **不支援**  -h [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]參數。 舊版 32 位元 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體使用此參數，在啟用 AWE 的狀況下保留 Hot Add Memory 中繼資料的虛擬記憶體位址空間。 如需詳細資訊，請參閱 [SQL Server 2016 中已停止的 SQL Server 功能](http://msdn.microsoft.com/library/0678bfbc-5d3f-44f4-89c0-13e8e52404da)。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 服務啟動選項](../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
