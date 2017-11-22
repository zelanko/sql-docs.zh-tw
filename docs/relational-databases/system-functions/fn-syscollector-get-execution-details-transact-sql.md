---
title: "f (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs: TSQL
helpviewer_keywords: fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd44ed098f4dbf15e529df6cbe4026d065dfa2a5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="fnsyscollectorgetexecutiondetails-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對指定的封裝，傳回符合 package_execution_id 的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 記錄 (sysssislog) 部分。 此資料表會針對封裝或它們的工作和容器在執行階段所產生的每個記錄項目，各包含一個資料列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>引數  
 *g _ i d*  
 執行記錄的本機唯一識別碼。 *g _ i d*是**int**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**int**|記錄項目的唯一識別碼。|  
|event|**sysname**|產生記錄項目的事件名稱。|  
|computer|**nvarchar**|產生記錄項目時，封裝執行所在的電腦。|  
|! 運算子之後|**nvarchar**|執行了產生記錄項目之封裝的人員或代理程式的使用者名稱。|  
|來源|**nvarchar**|產生記錄項目的可執行檔名稱。|  
|sourceid|**uniqueidentifier**|產生記錄項目之可執行檔的 GUID。|  
|executionid|**uniqueidentifier**|產生記錄項目之可執行檔執行個體的 GUID。|  
|starttime|**datetime**|封裝開始執行的時間。|  
|endtime|**datetime**|封裝完成的時間。|  
|datacode|**int**|識別記錄項目相關事件的整數值。 "0" 表示事件沒有提供任何識別碼。|  
|databytes|**image**|識別傳回值的位元組陣列。|  
|message|**nvarchar**|事件的描述以及與此事件相關的資訊。|  
  
## <a name="permissions"></a>Permissions  
 需要 SELECT 權限**dc_operator**。  
  
## <a name="see-also"></a>請參閱＜  
 [啟用封裝記錄中的 SQL Server 資料工具](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
