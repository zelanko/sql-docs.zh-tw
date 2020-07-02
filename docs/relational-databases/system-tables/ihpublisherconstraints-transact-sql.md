---
title: IHpublisherconstraints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fa87169a0988336e8a00537a76126120fb95d196
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773774"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **IHpublisherconstraints**系統資料表會針對使用目前散發者從非 SQL Server 發行者所複寫的每個條件約束，各包含一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|識別已發行的條件約束。|  
|**table_id**|**int**|從[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)識別條件約束所屬的資料表。|  
|**publisher_id**|**smallint**|識別發行資料行所在位置的非 SQL Server 發行者。|  
|**名稱**|**Sysname**|已發行之條件約束的名稱。|  
|**型別**|**nvarchar(255)**|來自[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)系統資料表的支援條件約束類型。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
