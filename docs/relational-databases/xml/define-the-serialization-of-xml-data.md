---
title: "定義 XML 資料的序列化 | Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- entitization rules [XML in SQL Server]
- serialization
- reparsing serialized XML structures
- encoding [XML in SQL Server]
- XML [SQL Server], serialization
- xml data type [SQL Server], serialization
- typed XML
ms.assetid: 42b0b5a4-bdd6-4a60-b451-c87f14758d4b
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17f11bc07868dd8f22cdf75f369de6e6ca952dc8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="define-the-serialization-of-xml-data"></a>定義 XML 資料的序列化
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 將 XML 資料類型明確或隱含轉換成 SQL 字串或二進位類型時，會根據本主題中所列的規則來序列化 XML 資料類型的內容。  
  
## <a name="serialization-encoding"></a>序列化編碼  
 如果 SQL 目標類型是 VARBINARY，其結果會以 UTF-16 序列化，前面有 UTF-16 位元組順序標示，但沒有 XML 宣告。 如果目標類型太小，則會引發錯誤。  
  
 例如：  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as VARBINARY(MAX))  
```  
  
 以下是結果：  
  
```  
0xFFFE3C0094032F003E00  
```  
  
 如果 SQL 目標類型是 NVARCHAR 或 NCHAR，則結果會以 UTF-16 序列化，但前面沒有位元組順序標示，也沒有 XML 宣告。 如果目標類型太小，則會引發錯誤。  
  
 例如：  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as NVARCHAR(MAX))  
```  
  
 以下是結果：  
  
```  
<Δ/>  
```  
  
 如果 SQL 目標類型是 VARCHAR 或 NCHAR，其結果會以對應於資料庫定序字碼頁的編碼序列化，但沒有位元組順序標示或 XML 宣告。 如果目標類型太小，或值無法對應至目標定序字碼頁，則會引發錯誤。  
  
 例如：  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as VARCHAR(MAX))  
```  
  
 如果目前定序的字碼頁無法表示 Unicode 字元 Δ，這樣會產生錯誤，否則會以特定編碼表示該字元。  
  
 將 XML 結果傳回至用戶端時，資料是以 UTF-16 編碼格式傳送。 接著，用戶端提供者會根據其 API 規則來公開此資料。  
  
## <a name="serialization-of-the-xml-structures"></a>XML 結構的序列化  
 **xml** 資料類型的內容以一般方式序列化。 特別是，元素節點是對應到元素標示，而文字節點則對應到文字內容。 不過，下列章節將描述字元在何種情況下實體化，以及具類型的不可部份完成值如何序列化。  
  
## <a name="entitization-of-xml-characters-during-serialization"></a>XML 字元在序列化期間的實體化  
 每一個已序列化的 XML 結構應該能夠加以重新剖析。 因此，有些字元必須以實體化方式來序列化，以透過 XML 剖析器的正規化階段保留字元的反覆存取功能。 不過，有些字元必須實體化，使文件能夠有完善的格式，以便加以剖析。 以下是在序列化期間所套用的實體化規則：  
  
-   若字元 &、\< 和 > 是出現在屬性值或元素內容中，則一律分別實體化成 &amp;、&lt; 和 &gt;。  
  
-   因為 SQL Server 使用引號 (U+0022) 來括住屬性值，所以屬性值中的引號會實體化成 &quot;。  
  
-   只在伺服器上進行轉換時，Surrogate 字組會實體化成單一數字字元參考。 例如，Surrogate 字組 U+D800 U+DF00 會實體化成數字字元參考 &\#x00010300;。  
  
-   為避免在剖析期間將定位字元 (U+0009) 和換行符號 (LF、U+000A) 正規化，已在屬性值內分別實體化成其數字字元參考 &\#x9; 和 &\#xA;。  
  
-   為避免在剖析期間將歸位字元 (CR、U+000D) 正規化，已在屬性值和元素內容內實體化成其數字字元參考 &\#xD;。  
  
-   為了保護只包含空格的文字節點，其中一個空格字元 (通常是最後一個) 會實體化為其數字字元參考。 如此一來，不論剖析期間的空格處理設定為何，重新剖析作業都會保留空格文字節點。  
  
 例如：  
  
```  
declare @u NVARCHAR(50)  
set @u = N'<a a="  
    '+NCHAR(0xD800)+NCHAR(0xDF00)+N'>">   '+NCHAR(0xA)+N'</a>'  
select CAST(CONVERT(XML,@u,1) as NVARCHAR(50))  
```  
  
 以下是結果：  
  
```  
<a a="  
    𐌀>">     
</a>  
```  
  
 如果您不想套用最後一個空格的保護規則，您可以在從 **XML** 轉換成字串或二進位類型時，使用明確的 CONVERT 選項 1。 例如，若要避免實體化，您可以執行下列動作：  
  
```  
select CONVERT(NVARCHAR(50), CONVERT(XML, '<a>   </a>', 1), 1)  
```  
  
 請注意， [query() 方法 (XML 資料類型)](../../t-sql/xml/query-method-xml-data-type.md) 會產生 XML 資料類型執行個體。 因此，轉換成字串或二進位類型的 **query()** 方法的任何結果，將根據前述規則而實體化。 如果您要取得未實體化的字串值，請改用 [value() 方法 (XML 資料類型)](../../t-sql/xml/value-method-xml-data-type.md) 。 以下是使用 **query()** 方法的範例：  
  
```  
declare @x xml  
set @x = N'<a>This example contains an entitized char: <.</a>'  
select @x.query('/a/text()')  
```  
  
 以下是結果：  
  
```  
This example contains an entitized char: <.  
```  
  
 以下是使用 **value()** 方法的範例：  
  
```  
select @x.value('(/a/text())[1]', 'nvarchar(100)')  
```  
  
 以下是結果：  
  
```  
This example contains an entitized char: <.  
```  
  
## <a name="serializing-a-typed-xml-data-type"></a>序列化 XML 類型的資料類型  
 具類型的 **xml** 資料類型執行個體根據其 XML 結構描述類型來包含具類型的值。 這些值根據其 XML 結構描述類型而序列化，並使用與 XQuery 轉換成 xs:string 時產生的相同格式。 如需詳細資訊，請參閱 [XQuery 中的類型轉換規則](../../xquery/type-casting-rules-in-xquery.md)。  
  
 例如，xs:double 值 1.34e1 序列化為 13.4，如下列範例所顯示：  
  
```  
declare @x xml  
set @x =''  
select CAST(@x.query('1.34e1') as nvarchar(50))  
```  
  
 這會傳回字串值 13.4。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 中的類型轉換規則](../../xquery/type-casting-rules-in-xquery.md)   
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
