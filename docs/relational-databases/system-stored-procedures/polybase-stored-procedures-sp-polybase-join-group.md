---
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b7be2bb99a92794ed8c1b5971edca47522c2552
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941931"
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  為計算節點將 PolyBase 向外延展計算群組的 SQL Server 執行個體。  
  
 SQL Server 執行個體必須具有[PolyBase](../../relational-databases/polybase/polybase-guide.md)安裝的功能。  PolyBase 可讓非 SQL Server 資料來源，例如 Hadoop 和 Azure blob 儲存體的整合。 另請參閱[sp_polybase_leave_group &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>引數  
 *@head_node_address* = N'*head_node_address*'  
 裝載 SQL Server PolyBase 向外延展群組的前端節點的電腦名稱。 *@head_node_address* 是 nvarchar(255)。  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 正在執行 PolyBase Data Movement Service 的前端節點的控制通道連接埠。 *@dms_control_channel_port* 是不帶正負號的 __int16。 預設值是**16450**。  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 前端節點的 SQL Server 執行個體，PolyBase 向外延展群組中的名稱。 *@head_node_sql_server_instance_name* 是 nvarchar(16)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="remarks"></a>備註  
 執行預存程序之後, 關閉 PolyBase engine，然後重新啟動 PolyBase Data Movement Service，在電腦上。 若要確認在前端節點上執行下列 DMV: **sys.dm_exec_compute_nodes**。  
  
## <a name="example"></a>範例  
 此範例為計算節點至 PolyBase 群組聯結目前的電腦。  在前端節點的名稱是**HST01**的前端節點上的 SQL Server 執行個體名稱，而且**MSSQLSERVER**。  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
