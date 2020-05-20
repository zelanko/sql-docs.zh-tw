---
title: IHindextypes （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHindextypes
- IHindextypes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHindextypes system table
ms.assetid: 5eb67d59-a19d-4dba-9d2b-657f87818f6b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6a448e118fcc6c6401f8e3632dc035b53209655e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82806089"
---
# <a name="ihindextypes-transact-sql"></a>IHindextypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHindextypes**系統資料表會針對非 SQL Server 發行者所支援的每個非 SQL Server 索引類型，各包含一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**type**|**nvarchar(255)**|支援的非 SQL Server 索引類型名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
