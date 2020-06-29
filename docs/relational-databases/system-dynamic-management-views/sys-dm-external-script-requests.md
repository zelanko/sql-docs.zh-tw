---
title: sys. dm_external_script_requests |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 80b468006ba3ec4c479514059b3b89f65e500b37
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469343"
---
# <a name="sysdm_external_script_requests"></a>sys.dm_external_script_requests
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

逐資料列傳回正在執行外部指令碼的每個使用中背景工作帳戶。
  
> [!NOTE]
> 只有當您已安裝並啟用支援外部腳本執行的功能時，才可以使用此動態管理檢視（DMV）。 如需詳細資訊，請參閱[SQL Server 2017 和更新版本中的 Machine Learning 服務（r、Python）](../../machine-learning/sql-server-machine-learning-services.md)、 [SQL Server 2016 中的 r SERVICES](../../machine-learning/r/sql-server-r-services.md)和[Azure SQL 受控執行個體中的 Machine Learning 服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**唯一識別碼**|傳送外部指令碼要求的處理序識別碼。 這會對應至收到 SQL 實例的處理序識別碼。|  
|語言|**nvarchar**|代表支援的指令碼語言的關鍵字。 |  
|degree_of_parallelism|**int**|指出已建立之平行處理序數目的數字。 這個值可能與已要求的平行處理序數目不同。|  
|external_user_name|**nvarchar**|用來執行指令碼的 Windows 背景工作帳戶。|  
  
## <a name="permissions"></a>權限

 需要 `VIEW SERVER STATE` 伺服器的許可權。  
  
> [!NOTE]
> 執行外部腳本的使用者必須具有額外的許可權 `EXECUTE ANY EXTERNAL SCRIPT` ，不過，沒有此許可權的系統管理員可以使用此 DMV。 
  
## <a name="remarks"></a>備註  

此檢視可使用指令碼語言識別碼進行篩選。

此檢視也會傳回正在執行指令碼的背景工作帳戶。 如需外部腳本所使用之背景工作帳戶的相關資訊，請參閱 SQL Server Machine Learning 服務中擴充性[架構的安全性總覽](../../machine-learning/concepts/security.md#sqlrusergroup)一節中所使用的身分識別（SQLRUserGroup）一節。

**external_script_request_id** 欄位中所傳回的 GUID 也代表暫存檔案儲存所在之安全目錄的檔案名稱。 每個背景工作帳戶，例如 MSSQLSERVER01，都代表單一 SQL 登入或 Windows 使用者，而且可能用來執行多個腳本要求。 根據預設，完成要求的指令碼之後，即會清除這些暫存檔案。

此 DMV 只會監視使用中處理序，而無法回報已完成的指令碼。 如果您需要追蹤指令碼的持續時間，建議您將計時資訊加入您的指令碼，然後當做指令碼執行的一部分來擷取該資訊。

## <a name="examples"></a>範例  
  
### <a name="viewing-the-currently-active-scripts-for-a-particular-process"></a>針對特定進程，查看目前作用中的腳本

 下列範例顯示目前執行個體上正在執行之外部指令碼的執行次數。  
  
```sql
SELECT external_script_request_id
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests;
```  

結果  

external_script_request_id  |語言  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01

## <a name="see-also"></a>另請參閱

+ [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [執行相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
