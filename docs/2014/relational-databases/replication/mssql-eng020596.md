---
title: MSSQL_ENG020596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddabe3e1a3a12e3aa14c5a6c641345d3236c2fe2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62938478"
---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|20596|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|只有 '%s' 或 db_owner 的成員可以卸除匿名的代理程式。|  
  
## <a name="explanation"></a>說明  
 您沒有足夠的權限卸除匿名訂閱的代理程式。 呼叫 [sp_dropanonymousagent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql) 時使用的登入必須是「散發者」端 **sysadmin** 固定伺服器角色的成員、散發資料庫中的 **db_owner** 固定資料庫角色的成員，或者該使用者必須是第一次執行代理程式時初始化的使用者。  
  
## <a name="user-action"></a>使用者動作  
 使用適當的認證登入，並執行 **sp_dropanonymousagent**。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
