---
title: sp_polybase_leave_group (Transact-sql) |Microsoft Docs
description: Sp_polybase_leave_group Transact-sql 命令會從 PolyBase 群組移除 SQL Server 實例，以進行相應放大計算。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2ce2e2ad16277c6ae5e21939976ede8ac89c8843
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546245"
---
# <a name="sp_polybase_leave_group-transact-sql"></a>sp_polybase_leave_group (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  從 PolyBase 群組移除 SQL Server 實例，以進行相應放大計算。 
 
 SQL Server 實例必須安裝  [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md) 功能。  PolyBase 可整合非 SQL Server 的資料來源，例如 Hadoop 和 Azure blob 儲存體。 另請參閱 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>權限  
 需要 CONTROL SERVER 許可權。  
  
## <a name="remarks"></a>備註  
 您只能從群組中移除計算節點。  
  
 執行預存程式之後，請重新開機 PolyBase 引擎，並在電腦上 PolyBase 資料移動服務。 若要確認在前端節點上執行下列 DMV： **sys. dm_exec_compute_nodes**。  
  
## <a name="example"></a>範例  
 此範例會從 PolyBase 群組中移除目前的電腦。  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
