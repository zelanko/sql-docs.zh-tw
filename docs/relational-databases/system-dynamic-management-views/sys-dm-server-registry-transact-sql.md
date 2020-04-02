---
title: 系統dm_server_registry(轉算-SQL) |微軟文件
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
ms.openlocfilehash: 8daa2d195ab1f4cf4602b9633394ed1705a3d7d2
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/01/2020
ms.locfileid: "80530820"
---
# <a name="sysdm_server_registry-transact-sql"></a>sys.dm_server_registry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回儲存在目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之 Windows 登錄中的組態和安裝資訊。 針對每個登錄機碼各傳回一個資料列。 使用動態管理檢視傳回所需資訊 (例如主機上可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路組態值。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|登錄機碼名稱。 可為 Null。|  
|value_name|**nvarchar(256)**|機碼值名稱。 這是註冊表編輯器**的名稱**列中顯示的專案。 可為 Null。|  
|value_data|**sql_variant**|索引鍵資料的值。 這是給定條目的註冊錶編輯器的數據**列中顯示的**值。 可為 Null。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
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
WHERE value_name = N'CurrentVersion';  
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
 [系統dm_server_services&#40;轉算-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  
