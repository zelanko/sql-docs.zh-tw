---
title: "Fulltextcatalogproperty 函數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 383eafdda02f402d1c398183bfedac6dde85d9ce
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="fulltextcatalogproperty-transact-sql"></a>FULLTEXTCATALOGPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中全文檢索目錄屬性的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
FULLTEXTCATALOGPROPERTY ('catalog_name' ,'property')  
```  
  
## <a name="arguments"></a>引數  
  
> [!NOTE]  
>  未來版本將移除下列屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **LogSize**和**PopulateStatus**。 請避免在新的開發工作中使用這些屬性，並規劃修改目前使用任何這些屬性的應用程式。  
  
 *catalog_name*  
 這是一個包含全文檢索目錄名稱的運算式。  
  
 *屬性*  
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
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，FULLTEXTCATALOGPROPERTY) 會在使用者不具有該物件任何權限時傳回 NULL。 如需詳細資訊，請參閱[sp_help_fulltext_catalogs &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md).  
  
## <a name="remarks"></a>備註  
 FULLTEXTCATALOGPROPERTY ('*catalog_name*'、'**IndexSize**') 只會尋找片段具有狀態 4 或 6 中所示[sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)。 這些片段是邏輯索引的一部分。 因此， **IndexSize**屬性會傳回邏輯索引大小。 不過，在索引合併期間，實際的索引大小可能會是其邏輯大小的兩倍。 若要尋找所耗用的全文檢索索引合併期間的實際大小，請使用[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)系統預存程序。 該程序會查看所有與全文檢索索引相關聯的片段。 如果您限制全文檢索目錄檔案的成長，而且未提供足夠的空間給合併處理使用，則全文檢索母體擴展可能會失敗。 在此情況下，FULLTEXTCATALOGPROPERTY ('catalog_name' ,'IndexSize') 會傳回 0，而且下列錯誤會寫入全文檢索記錄中：  
  
 `Error: 30059, Severity: 16, State: 1. A fatal error occurred during a full-text population and caused the population to be cancelled. Population type is: FULL; database name is FTS_Test (id: 13); catalog name is t1_cat (id: 5); table name t1 (id: 2105058535). Fix the errors that are logged in the full-text crawl log. Then, resume the population. The basic Transact-SQL syntax for this is: ALTER FULLTEXT INDEX ON table_name RESUME POPULATION.`  
  
 很重要的應用程式不要在緊密迴圈中，檢查等到**PopulateStatus**屬性變成閒置 （表示擴展已完成） 因為這會帶 CPU 循環離開資料庫和全文檢索搜尋處理程序和原因逾時。 此外，它通常是更好的選項，檢查對應**PopulateStatus**屬性在資料表層級**TableFullTextPopulateStatus** OBJECTPROPERTYEX 系統函數中。 OBJECTPROPERTYEX 中的這個屬性及其他新的全文檢索屬性，可提供更精細的全文檢索索引資料表相關資訊。 如需詳細資訊，請參閱 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回名稱為 `Cat_Desc` 的全文檢索目錄中之全文檢索索引項目數。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT fulltextcatalogproperty('Cat_Desc', 'ItemCount');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [FULLTEXTSERVICEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
  
  
