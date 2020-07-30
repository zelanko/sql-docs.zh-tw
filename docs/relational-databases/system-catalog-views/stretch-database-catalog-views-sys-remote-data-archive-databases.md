---
title: sys.databases remote_data_archive_databases （Transact-sql） |Microsoft Docs
description: 瞭解 remote_data_archive_databases sys.databases 如何針對儲存已啟用延展功能的本機資料庫中的每個遠端資料庫，各包含一個資料列。
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
ms.openlocfilehash: e192a70c1d8f46b7ad89844a3b38019ab6364cc1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248147"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>Stretch Database 目錄 Views-sys. remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  針對儲存已啟用延展功能之本機資料庫之資料的每個遠端資料庫，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|自動產生的遠端資料庫本機識別碼。|  
|**remote_database_name**|**sysname**|遠端資料庫的名稱。|  
|**data_source_id**|**int**|用來連接到遠端伺服器的資料來源|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
