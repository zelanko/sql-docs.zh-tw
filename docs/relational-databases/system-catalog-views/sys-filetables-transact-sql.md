---
title: sys.filetables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fff9e99a6e7fbd9e6e2e9490d8b67fce75586b6e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038339"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的每個 FileTable，各傳回一個資料列。 如需有關 FileTable 的詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。    
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**||物件識別碼。 在資料庫中，這是唯一的。<br /><br /> 如需詳細資訊， [j &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_enabled**|**bit**|1 = FileTable 處於「已啟用」狀態。|  
|**directory_name**|**varchar(255)**|FileTable 的根目錄名稱。|  
|**filename_collation_id**||這是針對 FileTable 定義的定序識別碼。|  
|**filename_collation_name**||這是針對 FileTable 定義的定序名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [管理 Filetable](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
