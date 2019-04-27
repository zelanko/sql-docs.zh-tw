---
title: 轉換非搜尋字伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5ddad15af74e45313d3e71b059fae36d166560
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808689"
---
# <a name="transform-noise-words-server-configuration-option"></a>轉換非搜尋字伺服器組態選項
  使用`transform noise words`伺服器組態選項來隱藏錯誤訊息，如果非搜尋字，也就是[停用字詞](../../relational-databases/search/full-text-search.md)，造成的布林運算傳回零個資料列的全文檢索查詢。 若全文檢索查詢使用的 CONTAINS 述詞中，布林運算或 NEAR 運算有包括非搜尋字，則這個選項很有幫助。 下表說明可能的值。  
  
|值|描述|  
|-----------|-----------------|  
|0|不轉換非搜尋字 (或停用字詞)。 當全文檢索查詢包含非搜尋字時，此查詢會傳回零個資料列，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會引發警告。 這是預設行為。<br /><br /> 請注意這項警告是執行階段警告。 因此，如果查詢中的全文檢索子句並未執行，就不會引發此警告。 若為本機查詢，只會引發一則警告，即使有多個全文檢索查詢子句也一樣。 若為遠端查詢，連結的伺服器可能不會轉送錯誤。因此，可能不會引發此警告。|  
|1|轉換非搜尋字 (或停用字詞)。 忽略這些字，並評估查詢的其餘部分。<br /><br /> 如果非搜尋字指定在鄰近詞彙中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將其移除。 例如，非搜尋字 `is` 會從 `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`中移除，將搜尋查詢轉換為 `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`。 請注意， `CONTAINS(<column_name>, 'NEAR(hello,is)')` 只會轉換成 `CONTAINS(<column_name>, hello)` ，因為只有一個有效的搜尋詞彙。|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>轉換非搜尋字設定效果  
 這一節將說明包含非搜尋字 "`the`" 的查詢行為 (在 `transform noise words` 的替代設定底下)。  假設範例全文檢索查詢字串會針對包含下列資料的資料表資料列執行：`[1, "The black cat"]`。  
  
> [!NOTE]  
>  所有的這類案例都可以產生非搜尋字警告。  
  
-   轉換非搜尋字設為 0：  
  
    |查詢字串|結果|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|無結果 ("`the`" AND "`cat`" 的行為是相同的)。|  
    |"`cat`" NEAR "`the`"|無結果 ("`the`" NEAR "`cat`" 的行為是相同的)。|  
    |"`the`" AND NOT "`black`"|搜尋支援|  
    |"`black`" AND NOT "`the`"|搜尋支援|  
  
-   轉換非搜尋字設為 1：  
  
    |查詢字串|結果|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|識別碼為 1 之資料列的叫用|  
    |"`cat`" NEAR "`the`"|識別碼為 1 之資料列的叫用|  
    |"`the`" AND NOT "`black`"|搜尋支援|  
    |"`black`" AND NOT "`the`"|識別碼為 1 之資料列的叫用|  
  
## <a name="example"></a>範例  
 下列範例會將 `transform noise words` 設定為 `1`。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
