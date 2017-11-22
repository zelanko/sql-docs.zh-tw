---
title: "(transact-sql) |Microsoft 文件"
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_xe_file_target_read_file_TSQL
- fn_xe_file_target_read_file
- sys.fn_xe_file_target_read_file_TSQL
- sys.fn_xe_file_target_read_file
dev_langs: TSQL
helpviewer_keywords:
- extended events [SQL Server], functions
- fn_xe_file_target_read_file function
- sys.fn_xe_file_target_read_file function
ms.assetid: cc0351ae-4882-4b67-b0d8-bd235d20c901
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 603253fffd3d3ea6d5a42b37f9d7f4fc8a3edccd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnxefiletargetreadfile-transact-sql"></a>sys.fn_xe_file_target_read_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  讀取擴充事件非同步檔案目標所建立的檔案。 系統會以 XML 格式針對每個資料列傳回一個事件。  
  
> [!WARNING]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]和[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]接受 XEL 與 XEM 格式產生的追蹤結果。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]擴充事件只支援 XEL 格式的追蹤結果。 我們建議您使用 SQL Server Management Studio 來讀取 XEL 格式的追蹤結果。    
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_xe_file_target_read_file ( path, mdpath, initial_file_name, initial_offset )  
```  
  
## <a name="arguments"></a>引數  
 *路徑*  
 要讀取之檔案的路徑。 *路徑*可包含萬元字元，包括檔案的名稱。 *路徑*是**nvarchar （260)**。 沒有預設值。 在 Azure SQL Database 的內容中，這個值會是 HTTP URL 至 Azure 儲存體中的檔案。
  
 *mdpath*  
 對應至所指定的檔案的中繼資料檔案的路徑*路徑*引數。 *mdpath*是**nvarchar （260)**。 沒有預設值。 從 SQL Server 2016 開始，這個參數可以指定為 null。
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]不需要*mdpath*參數。 但是，維護它是為了保留與舊版 SQL Server 產生之記錄檔之間的相容性。  
  
 *initial_file_name*  
 要讀取的第一個檔案*路徑*。 *initial_file_name*是**nvarchar （260)**。 沒有預設值。 如果**null**指定為引數中找到的所有檔案*路徑*讀取。  
  
> [!NOTE]  
>  *initial_file_name*和*initial_offset*是成對的引數。 如果您指定任何一個引數的值，就必須指定另一個引數的值。  
  
 *initial_offset*  
 用來指定先前所讀取的上個位移，並略過所有事件直到位移為止 (含)。 從指定的位移之後，開始事件列舉。 *initial_offset*是**bigint**。 如果**null**指定為將會讀取整個檔案的引數。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|module_guid|**uniqueidentifier**|事件模組 GUID。 不可為 Null。|  
|package_guid|**uniqueidentifier**|事件封裝 GUID。 不可為 Null。|  
|object_name|**nvarchar(256)**|事件的名稱。 不可為 Null。|  
|event_data|**nvarchar(max)**|事件內容 (XML 格式)。 不可為 Null。|  
|file_name|**nvarchar （260)**|包含此事件之檔案的名稱。 不可為 Null。|  
|file_offset|**bigint**|包含此事件之檔案中的區塊位移。 不可為 Null。|  
|timestamp_utc|**datetime2**|**適用於**:[!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br />日期和時間 （UTC 時區） 的事件。 不可為 Null。|  

  
## <a name="remarks"></a>備註  
 讀取大型結果集藉由執行**sys.fn_xe_file_target_read_file**中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]可能會導致錯誤。 使用**將結果存檔**模式 (**Ctrl + Shift + F**) 大型結果集匯出至檔案，並改為讀取具有另一個工具的檔案。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieving-data-from-file-targets"></a>A. 從檔案目標中擷取資料  
 下列範例會從所有檔案中取得所有資料列。 在這個範例中，檔案目標和中繼檔都位於 C:\ 磁碟機的追蹤資料夾中。  
  
```  
SELECT * FROM sys.fn_xe_file_target_read_file('C:\traces\*.xel', 'C:\traces\metafile.xem', null, null);  
```  
  
## <a name="see-also"></a>請參閱＜  
 [擴充的事件動態管理檢視](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [擴充的事件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
