---
description: 主動 Geo-Replication-sp_wait_for_database_copy_sync
title: sp_wait_for_database_copy_sync
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-dt-2019
ms.openlocfilehash: 8d453d6d3fa43226921aa6f5f0322b8f574a5e31
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97410765"
---
# <a name="active-geo-replication---sp_wait_for_database_copy_sync"></a>主動 Geo-Replication-sp_wait_for_database_copy_sync
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  這個程序的範圍為主要和次要資料庫之間的 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] 關聯性。 呼叫 **sp_wait_for_database_copy_sync** 會導致應用程式等候，直到作用中次要資料庫複寫及認可所有已認可的交易為止。 只在主資料庫上執行 **sp_wait_for_database_copy_sync** 。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
  
## <a name="syntax"></a>語法  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>引數  
 [ @target_server =] ' server_name '  
 主控作用中的次要資料庫的 SQL Database 伺服器名稱。 server_name 是 sysname，沒有預設值。  
  
 [ @target_database = ] 'database_name'  
 作用中的次要資料庫名稱。 database_name 是 sysname，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 傳回 0 代表成功，傳回錯誤碼代表失敗。  
  
 可能的錯誤情況包括：  
  
-   伺服器名稱或資料庫名稱遺失。  
  
-   找不到指定的伺服器名稱或資料庫的連結。  
  
-   互連連接遺失。 **sp_wait_for_database_copy_sync** 將會在連接逾時後傳回。  
  
## <a name="permissions"></a>權限  
 主要資料庫中的任何使用者都可以呼叫這個系統預存程序。 登入必須是同時位於主要和作用中次要資料庫的使用者。  
  
## <a name="remarks"></a>備註  
 在 **sp_wait_for_database_copy_sync** 呼叫之前認可的所有交易都會傳送至作用中次要資料庫。  
  
## <a name="examples"></a>範例  
 下列範例會叫用 **sp_wait_for_database_copy_sync** ，以確保所有交易都會認可至主資料庫 db0，並傳送到目標伺服器 ubfyu5ssyt 上的作用中次要資料庫。  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_continuous_copy_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [異地複寫動態管理檢視 (Dmv) 和功能 &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status](../system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)
  
  
