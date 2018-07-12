---
title: sys.remote_data_archive_databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 84234467e626e8168b0d0a9b2a29f5c9cb5ad70f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428227"
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
  
  
