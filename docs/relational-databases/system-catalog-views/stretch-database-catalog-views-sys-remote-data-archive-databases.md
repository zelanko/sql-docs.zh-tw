---
title: "sys.remote_data_archive_databases (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cd9f8e2841bff4fe1ab1bbc61a8ea100207e205e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stretch-database-catalog-views---sysremotedataarchivedatabases"></a>Stretch Database 目錄檢視-sys.remote_data_archive_databases
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個遠端資料庫會儲存從已啟用延展功能的本機資料庫的資料。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|自動產生本機識別碼的遠端資料庫。|  
|**remote_database_name**|**sysname**|遠端資料庫的名稱。|  
|**data_source_id**|**int**|用來連線到遠端伺服器的資料來源|  
  
## <a name="see-also"></a>請參閱＜  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
