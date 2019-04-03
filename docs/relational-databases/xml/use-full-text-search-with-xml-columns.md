---
title: 使用 XML 資料行進行全文檢索搜尋 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b342fff66d5e3ec955566963a4a31d1540a2853e
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513025"
---
# <a name="use-full-text-search-with-xml-columns"></a>使用 XML 資料行進行全文檢索搜尋
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  您可以在 XML 資料行上建立全文檢索索引，以檢索 XML 值的內容，但忽略 XML 標記。 元素標記會當做 Token 界限來使用。 其中會檢索下列項目：  
  
-   XML 元素的內容。  
  
-   僅限最上層元素之 XML 屬性的內容，除非這些值是數值。  
  
 在可能的情況下，您可以用下列方法將全文檢索搜尋與 XML 索引合併：  
  
1.  首先，使用 SQL 全文檢索搜尋來篩選出感興趣的 XML 值。  
  
2.  接著，查詢那些在 XML 資料行上使用 XML 索引的 XML 值。  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>範例將全文檢索搜尋與 XML 查詢合併  
 在 XML 資料行上建立全文檢索之後，下列查詢會確認 XML 值在書名中有包含 "custom" 這個字：  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 **contains()** 方法使用全文檢索來進一步設定在文件中任何地方含有 "custom" 這個字的 XML 值。 **exist()** 子句可確定 "custom" 這個字有出現在書名中。  
  
 使用 **contains()** 和 XQuery **contains()** 的全文檢索搜尋具有不同的語意。 後者是子字串相符項，前者則是使用詞幹的 token 相符項。 因此，如果該搜尋是要尋找書名中有 "run" 的字串，相符項中將會包含 "run"、"runs" 和 "running"，因為全文檢索 **contains()** 和 Xquery **contains()** 都滿足了。 然而，該查詢與書名中的 "customizable" 這個字不符，因為全文檢索 **contains()** 失敗，但滿足了 Xquery **contains()** 。 一般而言，只要子字串相符，則應移除全文檢索 **contains()** 子句。  
  
 此外，全文檢索搜尋會使用詞幹，但 XQuery **contains()** 是逐字比對的相符項。 下一個範例將舉例說明之間的差異。  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>範例使用詞幹對 XML 值進行全文檢索搜尋  
 在上個範例中執行的 XQuery **contains()** 檢查通常是無法排除的。 請考量這項查詢：  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 文件中的 "ran" 之所以能夠符合搜尋條件，是因為使用詞幹， 而且沒有使用 XQuery 來檢查搜尋內容。  
  
 當您使用全文檢索的 AXSD 來將 XML 分解成關聯式資料行時，在 XML 檢視上出現的 XPath 查詢就不會在基礎資料表上執行全文檢索搜尋。  
  
## <a name="see-also"></a>另請參閱  
 [XML 索引 &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
