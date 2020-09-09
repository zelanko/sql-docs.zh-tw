---
description: sp_fulltext_pendingchanges (Transact-SQL)
title: sp_fulltext_pendingchanges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6befa1abf7f427ab59c851fac9e51933ecc97bb7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538895"
---
# <a name="sp_fulltext_pendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對使用變更追蹤的指定資料表，傳回未處理的變更 (例如，暫止插入、更新和刪除)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>引數  
 *table_id*  
 資料表的識別碼。 如果資料表不是全文檢索索引，或者資料表沒有啟用變更追蹤，則會傳回錯誤。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**索引鍵**|*|這是來自指定資料表的全文檢索索引鍵值。|  
|**DocId**|**bigint**|這是對應至索引鍵值的內部文件識別碼 (DocId) 資料行。|  
|**狀態**|**int**|0 = 資料列會從全文檢索索引中移除。<br /><br /> 1 = 資料列會被編製成全文檢索索引。<br /><br /> 2 = 資料列是最新的。<br /><br /> -1 = 資料列是處於過渡 (批次，但未認可) 狀態，或是錯誤狀態。|  
|**DocState**|**tinyint**|這是內部文件識別碼 (DocId) 對應狀態資料行的原始傾印。|  
  
 <sup>* 資料類型 Key，與基底資料表中全文檢索索引鍵資料行的資料類型一樣。</sup>  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="remarks"></a>備註  
 如果沒有任何變更可以處理，就會傳回空的資料列集。  
  
 全文檢索搜尋查詢不會傳回 **Status** 值為0的資料列。 這是因為資料列已經從基底資料表中刪除，並且正在等候從全文檢索索引中刪除。  
  
 若要找出特定資料表有多少變更暫止，請使用 OBJECTPROPERTYEX 函數的 **TableFullTextPendingChanges** 屬性。  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋和語義搜尋預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
