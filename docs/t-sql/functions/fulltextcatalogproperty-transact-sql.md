---
title: FULLTEXTCATALOGPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FULLTEXTCATALOGPROPERTY_TSQL
- FULLTEXTCATALOGPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], properties
- FULLTEXTCATALOGPROPERTY function
- status information [SQL Server], full-text catalogs
ms.assetid: f841dc79-2044-4863-aff0-56b8bb61f250
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 58592c26b8d5747876eda424c225bc3eca013d60
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33054685"
---
# <a name="fulltextcatalogproperty-transact-sql"></a>FULLTEXTCATALOGPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中全文檢索目錄屬性的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
FULLTEXTCATALOGPROPERTY ('catalog_name' ,'property')  
```  
  
## <a name="arguments"></a>引數  
  
> [!NOTE]  
>  下列屬性會從未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中移除：**LogSize** 和 **PopulateStatus**。 請避免在新的開發工作中使用這些屬性，並規劃修改目前使用任何這些屬性的應用程式。  
  
 *catalog_name*  
 這是一個包含全文檢索目錄名稱的運算式。  
  
 *property*  
 這是一個包含全文檢索目錄屬性名稱的運算式。 下表列出各個屬性，並提供傳回資訊的描述。  
  
|屬性|描述|  
|--------------|-----------------|  
|**AccentSensitivity**|區分腔調字設定。<br /><br /> 0 = 不區分腔調字<br /><br /> 1 = 區分腔調字|  
|**IndexSize**|顯示全文檢索目錄的邏輯大小，以 MB 為單位。 包括語意關鍵片語和文件相似度索引的大小。<br /><br /> 如需詳細資訊，請參閱此主題稍後的「備註」。|  
|**ItemCount**|索引項目的數目，包括目錄中的所有全文檢索、關鍵片語和文件相似度索引|  
|**LogSize**|支援這個項目的目的，只是為了與舊版相容。 一律傳回 0。<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 搜尋服務全文檢索目錄的相關錯誤記錄組合集大小 (以位元組為單位)。|  
|**MergeStatus**|主要合併是否正在進行中。<br /><br /> 0 = 主要合併不在進行中<br /><br /> 1 = 主要合併在進行中|  
|**PopulateCompletionAge**|前次全文檢索索引擴展完成和 01/01/1990 00:00:00 之間的時差 (以秒為單位)。<br /><br /> 只更新完整和累加搜耙的這個項目。 如果未進行擴展，便傳回 0。|  
|**PopulateStatus**|0 = 閒置<br /><br /> 1 = 完整擴展進行中<br /><br /> 2 = 已暫停<br /><br /> 3 = 調整執行速度<br /><br /> 4 = 復原中<br /><br /> 5 = 已關閉<br /><br /> 6 = 累加擴展進行中<br /><br /> 7 = 正在建立索引<br /><br /> 8 = 磁碟已滿， 已暫停。<br /><br /> 9 = 變更追蹤|  
|**UniqueKeyCount**|全文檢索目錄中唯一索引鍵的數目。|  
|**ImportStatus**|是否正在匯入全文檢索目錄。<br /><br /> 0 = 沒有正在匯入全文檢索目錄。<br /><br /> 1 = 正在匯入全文檢索目錄。|  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，FULLTEXTCATALOGPROPERTY) 會在使用者不具有該物件任何權限時傳回 NULL。 如需詳細資訊，請參閱 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 FULLTEXTCATALOGPROPERTY ('*catalog_name*','**IndexSize**') 只會尋找具有狀態 4 或 6 的片段，如 [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md) 中所示。 這些片段是邏輯索引的一部分。 因此，**IndexSize** 屬性只會傳回邏輯索引大小。 不過，在索引合併期間，實際的索引大小可能會是其邏輯大小的兩倍。 若要找出全文檢索索引在合併期間所使用的實際大小，請使用 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 系統預存程序。 該程序會查看所有與全文檢索索引相關聯的片段。 如果您限制全文檢索目錄檔案的成長，而且未提供足夠的空間給合併處理使用，則全文檢索母體擴展可能會失敗。 在此情況下，FULLTEXTCATALOGPROPERTY ('catalog_name' ,'IndexSize') 會傳回 0，而且下列錯誤會寫入全文檢索記錄中：  
  
 `Error: 30059, Severity: 16, State: 1. A fatal error occurred during a full-text population and caused the population to be cancelled. Population type is: FULL; database name is FTS_Test (id: 13); catalog name is t1_cat (id: 5); table name t1 (id: 2105058535). Fix the errors that are logged in the full-text crawl log. Then, resume the population. The basic Transact-SQL syntax for this is: ALTER FULLTEXT INDEX ON table_name RESUME POPULATION.`  
  
 應用程式不會在緊湊的迴圈中等待檢查 **PopulateStatus** 屬性是否成為閒置 (表示填入已完成)，因為這會使 CPU 循環離開資料庫和全文檢索搜尋處理序，而造成逾時。 另外，在資料表層級上檢查對應的 **PopulateStatus** 屬性 (OBJECTPROPERTYEX 系統函式中的 **TableFullTextPopulateStatus**) 通常是比較好的選擇。 OBJECTPROPERTYEX 中的這個屬性及其他新的全文檢索屬性，可提供更精細的全文檢索索引資料表相關資訊。 如需詳細資訊，請參閱 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回名稱為 `Cat_Desc` 的全文檢索目錄中之全文檢索索引項目數。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT fulltextcatalogproperty('Cat_Desc', 'ItemCount');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [中繼資料函式 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
  
  
