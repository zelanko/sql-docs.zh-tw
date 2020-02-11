---
title: 快照集。 fn_trace_getdata （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: rothja
ms.author: jroth
ms.openlocfilehash: a85a911d4c9f5cd4565e9839f3be44a4e2366079
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067747"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個函數會傳回針對指定之追蹤所擷取的所有事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>引數  
 *trace_info_id*  
 快照集中主要金鑰的唯一識別碼。 trace_info 管理資料倉儲資料庫中的資料表。 *trace_info_id*為**int**。  
  
 *start_time*  
 啟動追蹤的時間。 *start_time*為**datetime**。  
  
 *end_time*  
 結束追蹤的時間。 *end_time*為**datetime**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|\<> 的所有追蹤資料行|\<> 變化|管理資料倉儲資料庫內 snapshots.trace_data 資料表中的追蹤資料。<br /><br /> 您可以使用下列查詢取得指定之追蹤的資料行清單：<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **注意：** 快照集所傳回的資料行。 fn_trace_gettable 函式會對應到 sys.databases trace_columns 系統檢視中 [名稱] 欄中的值。 唯一的差異在於此函數不會傳回 GroupID 資料行。|  
  
## <a name="permissions"></a>權限  
 需要 mdw_reader 的 SELECT 權限。  
  
## <a name="see-also"></a>另請參閱  
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
