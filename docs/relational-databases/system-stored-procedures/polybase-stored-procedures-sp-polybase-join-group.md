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
ms.openlocfilehash: ba22ffe282e6b4248ed58bed850bc6ac08255df5
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278109"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  將 SQL Server 實例當做計算節點加入至 PolyBase 群組，以進行相應放大計算。  
  
 SQL Server 實例必須安裝[PolyBase](../../relational-databases/polybase/polybase-guide.md)功能。  PolyBase 可整合非 SQL Server 的資料來源，例如 Hadoop 和 Azure blob 儲存體。 另請[參閱&#40;sp_polybase_leave_group transact-sql&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>引數  
 *\@head_node_address* = N '*head_node_address*'  
 裝載 PolyBase 向外延展群組之 SQL Server 前端節點的電腦名稱稱。 *\@head_node_address*是 Nvarchar （255）。  
  
 *\@dms_control_channel_port* = dms_control_channel_port  
 前端節點 PolyBase 資料移動服務的控制通道執行所在的埠。 *@no__t 1dms_control_channel_port*是不帶正負號的 __int16。 預設值為**16450**。  
  
 *\@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 在 PolyBase 向外延展群組中，SQL Server 實例的前端節點名稱。 *\@head_node_sql_server_instance_name*是 Nvarchar （16）。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="remarks"></a>備註  
 執行預存程式之後，請關閉 PolyBase 引擎，然後重新開機電腦上的 PolyBase 資料移動服務。 若要確認在前端節點上執行下列 DMV： **sys.databases _exec_compute_nodes**。  
  
## <a name="example"></a>範例  
 此範例會將目前的電腦當做計算節點加入至 PolyBase 群組。  前端節點的名稱是**HST01** ，而前端節點上 SQL Server 實例的名稱是**MSSQLSERVER**。  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
