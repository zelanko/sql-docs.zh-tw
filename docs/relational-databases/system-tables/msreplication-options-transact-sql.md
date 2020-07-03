---
title: MSreplication_options （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 98d25db72c7067147a34fa21b0bfa8da16ae1d3e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889446"
---
# <a name="msreplication_options-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplication_options**資料表會儲存複寫在內部使用的中繼資料。 此資料表會儲存在**master**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|僅供內部使用。|  
|**value**|**bit**|僅供內部使用。|  
|**major_version**|**int**|僅供內部使用。|  
|**minor_version**|**int**|僅供內部使用。|  
|**修正**|**int**|僅供內部使用。|  
|**install_failures**|**int**|僅供內部使用。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
