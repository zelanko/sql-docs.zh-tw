---
title: sys.remote_data_archive_databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 74a44e8c3e6b0be026ac716d43b539869345b3b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945615"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivedatabases"></a>Stretch Database 目錄檢視-sys.remote_data_archive_databases
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個遠端資料庫會儲存從已啟用延展功能的本機資料庫的資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|自動產生區域識別項的遠端資料庫。|  
|**remote_database_name**|**sysname**|遠端資料庫的名稱。|  
|**data_source_id**|**int**|用來連線到遠端伺服器的資料來源|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
