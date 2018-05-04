---
title: sys.sequences (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sequences_TSQL
- sys.sequences
- sequences
- sequences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sys. sequences catalog view
- sys.sequences catalog view
ms.assetid: 0e1b0e32-1cce-40f7-83c8-860ec660138a
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3c8e29f964ce7c28ccde727b7ffb3ca5bfad3e14
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="syssequences-transact-sql"></a>sys.sequences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對資料庫中的每個順序物件包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|\<繼承資料行 >||繼承的所有資料行[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**start_value**|**sql_variant NOT NULL**|順序物件的起始值。 如果順序物件是藉由使用 ALTER SEQUENCE 重新啟動，它會從這個值重新啟動。 當順序物件循環其繼續進行**minimum_value**或**maximum_value**，而非**start_value**。|  
|**increment**|**sql_variant NOT NULL**|每次產生值之後，用來遞增順序物件的值。|  
|**minimum_value**|**sql_variant NULL**|可由順序物件產生的最小值。 達到此值之後，順序物件在嘗試產生更多的值時會傳回錯誤，如果已指定 CYCLE 選項則會重新啟動。 如果未指定 MINVALUE，此資料行會傳回順序產生器的資料類型所支援的最小值。|  
|**maximum_value**|**sql_variant NULL**|可由順序物件產生的最大值。 達到此值之後，順序物件在嘗試產生更多的值時會開始傳回錯誤，如果已指定 CYCLE 選項則會重新啟動。 如果未指定 MAXVALUE，此資料行會傳回順序物件的資料類型所支援的最大值。|  
|**is_cycling**|**位元 NOT NULL**|如果已為順序物件指定 NO CYCLE，則傳回 0，如果已指定 CYCLE 則傳回 1。|  
|**is_cached**|**位元 NOT NULL**|如果已為順序物件指定 NO CACHE，則傳回 0，如果已指定 CACHE 則傳回 1。|  
|**cache_size**|**int NULL**|傳回順序物件的指定快取大小。 如果以 NO CACHE 選項建立順序，或如果指定 CACHE 但未指定快取大小，此資料行會包含 NULL。 如果快取大小所指定的值大於順序物件可傳回之值的數目上限，仍然會顯示該無法取得的快取大小。|  
|**system_type_id**|**tinyint NOT NULL**|順序物件之資料類型的系統類型識別碼。|  
|**user_type_id**|**int NOT NULL**|如使用者所定義，順序物件的資料類型識別碼。|  
|**有效位數**|**tinyint NOT NULL**|資料類型的最大有效位數。|  
|**scale**|**tinyint NOT NULL**|資料類型的最大小數位數。 小數位數會與有效位數一起傳回，提供使用者完整的中繼資料。 順序物件的小數位數永遠是 0，因為只允許整數類型。|  
|**current_value**|**sql_variant NOT NULL**|最後一個強制值。 也就是從最新的執行 NEXT VALUE FOR 函式或執行的最後一個值傳回的值**sp_sequence_get_range**程序。 如果從未使用順序，則會傳回 START WITH 值。|  
|**is_exhausted**|**位元 NOT NULL**|0 表示可從順序產生多個值。 1 表示順序物件已經達到 MAXVALUE 參數，而且順序未設定為 CYCLE。 NEXT VALUE FOR 函數會傳回錯誤，直到使用 ALTER SEQUENCE 重新啟動順序為止。|  
  
## <a name="permissions"></a>Permissions  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本中，目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
