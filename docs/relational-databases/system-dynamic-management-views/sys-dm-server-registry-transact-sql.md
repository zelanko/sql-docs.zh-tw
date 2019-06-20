---
title: sys.dm_server_registry (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_registry_TSQL
- sys.dm_server_registry
- dm_server_registry
- sys.dm_server_registry_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_registry dynamic management view
ms.assetid: 9b3e0c74-2e99-4996-a383-104d51831e97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e4e0b1069977c14216952e537d4bd12b28190529
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62684006"
---
# <a name="sysdmserverregistry-transact-sql"></a>sys.dm_server_registry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回儲存在目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之 Windows 登錄中的組態和安裝資訊。 針對每個登錄機碼各傳回一個資料列。 使用動態管理檢視傳回所需資訊 (例如主機上可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路組態值。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|登錄機碼名稱。 可為 Null。|  
|value_name|**nvarchar(256)**|機碼值名稱。 這是所示的項目**名稱**資料行的登錄編輯程式。 可為 Null。|  
|value_data|**sql_variant**|索引鍵資料的值。 這是所顯示的值**資料**資料行的指定項目 登錄編輯器。 可為 Null。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-display-the-sql-server-services"></a>A. 顯示 SQL Server 服務  
 下列範例會傳回目前 SQL Server 執行個體之 SQL Server 及 SQL Server Agent 服務的登錄機碼值。  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%ControlSet%';  
```  
  
### <a name="b-display-the-sql-server-agent-registry-key-values"></a>B. 顯示 SQL Server Agent 登錄機碼值  
 下列範例會傳回目前 SQL Server 執行個體的 SQL Server Agent 登錄機碼值。  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SQLAgent%';  
```  
  
### <a name="c-display-the-current-version-of-the-instance-of-sql-server"></a>C. 顯示目前 SQL Server 執行個體的版本  
 下列範例會傳回目前 SQL Server 執行個體的版本。  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key = N'CurrentVersion';  
```  
  
### <a name="d-display-the-parameters-passed-to-the-instance-of-sql-server-during-startup"></a>D. 顯示啟動時傳遞給 SQL Server 執行個體的參數  
 下列範例會傳回啟動時傳遞給 SQL Server 執行個體的參數。  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%Parameters';  
```  
  
### <a name="e-return-network-configuration-information-for-the-instance-of-sql-server"></a>E. 傳回 SQL Server 執行個體的網路組態資訊  
 下列範例會傳回目前 SQL Server 執行個體的網路組態值。  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SuperSocketNetLib%';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_server_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  
