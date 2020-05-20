---
title: sp_polybase_leave_group （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4e9f5e12a56fe825909dd991c4b3253d3d90608c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827822"
---
# <a name="sp_polybase_leave_group-transact-sql"></a>sp_polybase_leave_group （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  從 PolyBase 群組中移除 SQL Server 實例，以進行相應放大計算。 
 
 SQL Server 實例必須安裝[PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)功能。  PolyBase 可整合非 SQL Server 的資料來源，例如 Hadoop 和 Azure blob 儲存體。 另請參閱[sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)。  
  
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
  
 執行預存程式之後，請重新開機 PolyBase 引擎並在電腦上 PolyBase 資料移動服務。 若要確認在前端節點上執行下列 DMV： **sys. dm_exec_compute_nodes**。  
  
## <a name="example"></a>範例  
 此範例會從 PolyBase 群組中移除目前的電腦。  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
