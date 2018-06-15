---
title: snapshots.fn_trace_getdata (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0c6abb9a761023cca125ffae381ea8c72b0582d6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33232497"
---
# <a name="snapshotsfntracegetdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個函數會傳回針對指定之追蹤所擷取的所有事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>引數  
 *trace_info_id*  
 在 管理資料內 snapshots.trace_info 資料表的主索引鍵的唯一識別碼倉儲資料庫。 *trace_info_id*是**int**。  
  
 *start_time*  
 啟動追蹤的時間。 *start_time*是**datetime**。  
  
 *end_time*  
 結束追蹤的時間。 *end_time*是**datetime**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|\<所有的追蹤資料行 >|\<變化 >|管理資料倉儲資料庫內 snapshots.trace_data 資料表中的追蹤資料。<br /><br /> 您可以使用下列查詢取得指定之追蹤的資料行清單：<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **注意：** snapshots.fn_trace_gettable 函數所傳回的資料行對應到 sys.trace_columns 系統檢視表中的 [名稱] 欄中的值。 唯一的差異在於此函數不會傳回 GroupID 資料行。|  
  
## <a name="permissions"></a>Permissions  
 需要 mdw_reader 的 SELECT 權限。  
  
## <a name="see-also"></a>另請參閱  
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
