---
title: sys.databases _external_script_execution_stats |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_execution_stats
- sys.dm_external_script_execution_stats_TSQL
- dm_external_script_execution_stats
- dm_external_script_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_execution_stats dynamic management view
ms.assetid: 2e99f026-ceb2-42a2-a549-c71d31ed0cf4
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 314318f2292a8d929a5d0eeaf68f01910f6de45f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476285"
---
# <a name="sysdmexternalscriptexecutionstats"></a>sys.dm_external_script_execution_stats
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

逐資料列傳回各種類型的外部指令碼要求。 外部指令碼要求會依支援的外部指令碼語言分組。 針對每個註冊的外部指令碼函數，會產生一個資料列。 除非是由父處理序 (例如 `rxExec`) 送出，否則不會記錄任何外部指令碼函數。
  
> [!NOTE]  
> 只有當您已安裝並啟用支援外部腳本執行的功能時, 才可以使用此動態管理檢視 (DMV)。 如需詳細資訊, 請參閱[SQL Server 2017 和更新版本中 SQL Server 2016 和 Machine Learning 服務 (R、Python)](../../advanced-analytics/what-is-sql-server-machine-learning.md)[中的 R Services](../../advanced-analytics/r/sql-server-r-services.md) 。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|language|**nvarchar**|註冊的外部指令碼語言名稱。 每個外部指令碼必須在指令碼要求中指定語言，才能啟動相關聯的啟動程式。 |  
|counter_name|**nvarchar**|註冊的外部指令碼函數名稱。 不可為 Null。|  
|counter_value|**integer**|伺服器上已呼叫之註冊的外部指令碼函數總數。 這個值會從在執行個體上安裝功能之後開始累計，而且無法重設。|  

  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
> [!NOTE]  
>  執行外部指令碼的使用者必須具有額外的權限 EXECUTE ANY EXTERNAL SCRIPT，但系統管理員可以在沒有此權限的情況下使用此 DMV。 
  
## <a name="remarks"></a>備註  
  此 DMV 的提供是為了讓內部遙測可以監視 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中所提供之新外部指令碼執行功能的整體使用狀況。 遙測服務會隨著 LaunchPad 一起啟動，並在每次呼叫註冊的外部指令碼函數時遞增以磁碟為基礎的計數器。

一般而言，只要產生效能計數器的處理序正在使用，效能計數器就會有效。 因此，DMV 上的查詢無法顯示已停止執行之服務的詳細資料。 例如, 如果啟動器執行外部腳本, 但很快就會完成, 則傳統 DMV 可能不會顯示任何資料。

因此，此 DMV 所追蹤的計數器會持續執行，並透過寫入磁碟來保留 sys.dm_external_script_requests 的狀態，即使執行個體已關閉亦然。

   
  
### <a name="counter-values"></a>計數器值
在 SQL Server 2016 中, 唯一支援的外部語言是 R, 而外部腳本要求則[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]是由處理。 在 SQL Server 2017 中, R 和 Python 都是支援的外部語言, 而外部腳本要求則[!INCLUDE[rsql_productname_md](../../includes/rsql-productnamenew-md.md)]是由處理。

針對 R, 此 DMV 會追蹤在實例上所進行的 R 呼叫數目。 例如，如果呼叫 `rxLinMod` 並以平行方式執行，此計數器會遞增 1。
 
針對 R 語言， *counter_name* 欄位中所顯示的計數器值代表所註冊之 ScaleR 函數的名稱。 *counter_value* 欄位中的值代表特定 ScaleR 函數執行個體的累計數目。 

針對 Python, 此 DMV 會追蹤在實例上所進行的 Python 呼叫數目。

該數目會在執行個體上安裝並啟用此功能之後開始計算，並累計到系統管理員刪除或覆寫維護狀態的檔案為止。 因此，通常無法重設 *counter_value*中的值。 如果您想要依工作階段、行事曆時間或其他間隔監視使用狀況，建議您將計數擷取至資料表。

### <a name="registration-of-external-script-functions-in-r"></a>在 R 中註冊外部腳本函式

R 支援任意腳本, 而 R 群組提供數千個封裝, 每個套件都有自己的函式和方法。 不過，此 DMV 只會監視隨 SQL Server R Services 安裝的 ScaleR 函數。

安裝此功能時會執行這些函數的註冊，而且無法加入或刪除已註冊的函數。

## <a name="examples"></a>範例  
  
### <a name="viewing-the-number-of-r-scripts-run-on-the-server"></a>檢視伺服器上執行的 R 指令碼數目  
 下列範例顯示 R 語言之外部指令碼執行的累計次數。  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'R';
```  

### <a name="viewing-the-number-of-python-scripts-run-on-the-server"></a>查看伺服器上執行的 Python 腳本數目  
 下列範例會顯示 Python 語言的外部腳本執行累計數目。  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'Python';
```  

  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md) 
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

