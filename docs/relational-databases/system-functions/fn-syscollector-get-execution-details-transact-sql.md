---
title: fn_syscollector_get_execution_details （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
author: rothja
ms.author: jroth
ms.openlocfilehash: 44180a30c69a8da47cfad77c07f86ee6b9b8bfaa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775178"
---
# <a name="fn_syscollector_get_execution_details-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  針對指定的封裝，傳回符合 package_execution_id 的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 記錄 (sysssislog) 部分。 此資料表會針對封裝或它們的工作和容器在執行階段所產生的每個記錄項目，各包含一個資料列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>引數  
 *log_id*  
 執行記錄的本機唯一識別碼。 *log_id*為**int**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**int**|記錄項目的唯一識別碼。|  
|event|**sysname**|產生記錄項目的事件名稱。|  
|computer|**nvarchar**|產生記錄項目時，封裝執行所在的電腦。|  
|! 運算子之後|**nvarchar**|執行了產生記錄項目之封裝的人員或代理程式的使用者名稱。|  
|source|**nvarchar**|產生記錄項目的可執行檔名稱。|  
|sourceid|**uniqueidentifier**|產生記錄項目之可執行檔的 GUID。|  
|executionid|**uniqueidentifier**|產生記錄項目之可執行檔執行個體的 GUID。|  
|starttime|**datetime**|封裝開始執行的時間。|  
|endtime|**datetime**|封裝完成的時間。|  
|datacode|**int**|識別記錄項目相關事件的整數值。 "0" 表示事件沒有提供任何識別碼。|  
|databytes|**image**|識別傳回值的位元組陣列。|  
|message|**nvarchar**|事件的描述以及與此事件相關的資訊。|  
  
## <a name="permissions"></a>權限  
 需要**dc_operator**的 SELECT 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [啟用 SQL Server Data Tools 中的封裝記錄功能](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
