---
description: 'sp_polybase_join_group (Transact-sql) '
title: sp_polybase_join_group |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6e9e76c30adf6ec3ec241c5f5bc8589802a2cad0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489678"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  將 SQL Server 實例作為計算節點新增至 PolyBase 群組以進行向外延展計算。  
  
 SQL Server 實例必須安裝  [PolyBase](../../relational-databases/polybase/polybase-guide.md) 功能。  PolyBase 可整合非 SQL Server 的資料來源，例如 Hadoop 和 Azure blob 儲存體。 另請參閱 [sp_polybase_leave_group &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>引數  
 * \@ head_node_address* = N '*head_node_address*'  
 裝載 PolyBase 向外延展群組 SQL Server 前端節點的電腦名稱稱。 * \@ head_node_address*是 Nvarchar (255) 。  
  
 * \@ dms_control_channel_port* = dms_control_channel_port  
 前端節點的控制通道 PolyBase 資料移動服務執行所在的埠。 * \@ dms_control_channel_port*是不帶正負號的 __int16。 預設值為 **16450**。  
  
 * \@ head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 在 PolyBase 向外延展群組中，前端節點 SQL Server 實例的名稱。 * \@ head_node_sql_server_instance_name*是 Nvarchar (16) 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>權限  
 需要 CONTROL SERVER 權限。  
  
## <a name="remarks"></a>備註  
 執行預存程式之後，請關閉 PolyBase 引擎，然後重新開機電腦上的 PolyBase 資料移動服務。 若要確認在前端節點上執行下列 DMV： **sys. dm_exec_compute_nodes**。  
  
## <a name="example"></a>範例  
 此範例會將目前的電腦作為計算節點加入至 PolyBase 群組。  前端節點的名稱是 **HST01** ，而前端節點上 SQL Server 實例的名稱是 **MSSQLSERVER**。  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
