---
description: sysarticlecolumns (Transact-SQL)
title: sysarticlecolumns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 45cc5fc3a39f13f7795e2f26aa91a15b618e2d38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460233"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns**資料表會針對快照式或交易式發行集中發行的每個資料表資料行，各包含一個資料列，並將每個資料行對應到它的發行項。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**>artid**|**int**|識別發行項。|  
|**colid**|**smallint**|識別發行項中的資料行。|  
|**is_udt**|**bit**|指出資料行是否為使用者自訂資料類型 (UDT) 資料行。 值為 **1** 表示 UDT 資料行。|  
|**is_xml**|**bit**|指出資料行是否為 **xml** 資料行。 值為 **1** 表示 xml 資料行。|  
|**is_max**|**bit**|指出資料行是否為大數值資料類型資料行、 **Varchar (max) **、 **Nvarchar (max) **和 **Varbinary (max) **。 值為 **1** 表示大型值資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
