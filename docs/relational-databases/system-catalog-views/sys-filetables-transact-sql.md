---
title: filetable （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d83b58f8ff153583775e2e321c5524b43b205745
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738768"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的每個 FileTable，各傳回一個資料列。 如需有關 FileTable 的詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。    
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id||物件識別碼。 在資料庫中，這是唯一的。<br /><br /> 如需詳細資訊，請[&#40;transact-sql&#41;的 sys.databases ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_enabled**|**bit**|1 = FileTable 處於「已啟用」狀態。|  
|**directory_name**|**varchar(255)**|FileTable 的根目錄名稱。|  
|**filename_collation_id**||這是針對 FileTable 定義的定序識別碼。|  
|**filename_collation_name**||這是針對 FileTable 定義的定序名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [管理 Filetable](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
