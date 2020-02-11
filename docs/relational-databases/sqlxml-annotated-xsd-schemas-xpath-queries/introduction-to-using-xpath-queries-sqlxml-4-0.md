---
title: 使用 XPath 查詢的簡介（SQLXML）
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f82c330e2d18f05d0f358171a4ffeabc63ac9c3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246587"
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>使用 XPath 查詢的簡介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以將 XML 路徑語言 (XPath) 查詢指定成 URL 的一部分或在範本中指定此查詢。 對應結構描述會決定這個產生片段的結構，而且系統會從資料庫中擷取值。 這個程序在概念上類似於使用 CREATE VIEW 陳述式來建立檢視，然後針對它們撰寫 SQL 查詢。  
  
> [!NOTE]  
>  若要了解 SQLXML 4.0 中的 XPath 查詢，您必須熟悉 XML 檢視和相關的概念，例如範本與對應結構描述。 如需詳細資訊，請參閱[批註式 XSD 架構簡介 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)，以及全球資訊網協會（W3C）所定義的 XPath 標準。  
  
 XML 文件是由元素節點、屬性節點、文字節點等節點所組成。 例如，請考慮下列 XML 文件：  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 在本檔中， ** \<客戶>** 是元素節點， **cid**是屬性節點，而「**重要**」則是文位元組點。  
  
 XPath 是一種圖表導覽語言，可用來從 XML 文件中選取一組節點。 每個 XPath 運算子都會根據前一個 XPath 運算子所選取的節點集來選取節點集。 例如，假設有一組** \<客戶>** 節點，則 XPath 可以選取**日期**屬性值為 **"7/14/1999"** 的所有** \<Order>** 節點。 產生的節點集會包含訂單日期為 7/14/1999 的所有訂單。  
  
 全球資訊網協會 (W3C) 將 XPath 語言定義成標準導覽語言。 SQLXML 4.0 會執行 W3C XPath 規格的子集，其位於http://www.w3.org/TR/1999/PR-xpath-19991008.html。  
  
 下面是 W3C XPath 實作與 SQLXML 4.0 實作之間的重要差異。  
  
-   **根目錄查詢**  
  
     SQLXML 4.0 不支援根目錄查詢 (/)。 每個 XPath 查詢都必須從架構中的最上層** \<ElementType>** 開始。  
  
-   **報告錯誤**  
  
     W3C XPath 規格沒有定義任何錯誤條件。 無法選取任何節點的 XPath 查詢會傳回空的節點集。 在 SQLXML 4.0 中，查詢可能會傳回許多錯誤訊息類型。  
  
-   **文件順序**  
  
     在 SQLXML 4.0 中，不一定會決定文件順序。 因此，不會實作為使用檔順序的數值述詞和軸（如**下列**所示）。  
  
     缺少文件順序也就表示只有當節點對應至單一資料列中的單一資料行時，才能夠評估該節點的字串值。 具有子元素的元素或是 IDREFS 或 NMTOKENS 節點無法轉換成字串。  
  
    > [!NOTE]  
    >  在某些情況下，來自**關聯**性注釋的索引**鍵欄位**批註或索引鍵，可能會產生具決定性的檔順序。 不過，這不是這些批註的主要使用，如需詳細資訊，請參閱[使用 sql：索引鍵欄位識別索引鍵資料行 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)和[使用 Sql： relationship 指定關聯性 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)。  
  
-   **資料類型**  
  
     SQLXML 4.0 在執行 XPath**字串**、**數位**和**布林**資料類型方面有一些限制。 如需詳細資訊，請參閱[&#40;SQLXML 4.0&#41;的 XPath 資料類型](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)。  
  
-   **交叉乘積查詢**  
  
     SQLXML 4.0 不支援交叉乘積 XPath 查詢，例如 `Customers[Order/@OrderDate=Order/@ShipDate]`。 這個查詢會選取 OrderDate 等於 ShipDate 之任何訂單的所有客戶。  
  
     不過，SQLXML 4.0 支援 `Customer[Order[@OrderDate=@ShippedDate]]` 等查詢，其中系統會刪除 OrderDate 等於其 ShipDate 之任何訂單的客戶。  
  
-   **錯誤處理和安全性**  
  
     根據所使用的結構描述和 XPath 查詢運算式，在特定條件下，[!INCLUDE[tsql](../../includes/tsql-md.md)] 錯誤可能會公開給使用者。  
  
 下列各節中的表格會提供有關在 SQLXML 4.0 中實作 XPath 查詢與 W3C 規格的差異之處。  
  
## <a name="supported-functionality"></a>支援的功能  
 下表將顯示在 SQLXML 4.0 中實作之 XPath 語言的功能。  
  
|功能|Item|範例查詢的連結|  
|-------------|----------|----------------------------|  
|軸|**attribute**、 **child**、 **parent**和**self**軸|[在 XPath 查詢中指定軸 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|布林值述詞，包括連續和巢狀述詞||[在 XPath 查詢中指定算術運算子 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|所有關係運算子|=、！ =、<、 \<=、>、>=|[在 XPath 查詢中指定關聯式運算子 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|算術運算子|+、-、*、div|[在 XPath 查詢中指定算術運算子 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|明確轉換函數|**number （）**、 **string （）**、 **Boolean （）**|[在 XPath 查詢中指定明確轉換函數 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|布林運算子|AND、OR|[在 XPath 查詢中指定布林運算子 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|布林函數|**true （）**、 **false （）**、 **not （）**|[在 &#40;SQLXML 4.0&#41;的 XPath 查詢中指定布耳函數](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|XPath 變數||[在 XPath 查詢中指定 XPath 變數 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>不支援的功能  
 下表將顯示沒有在 SQLXML 4.0 中實作之 XPath 語言的功能。  
  
|功能|Item|  
|-------------|----------|  
|軸|**上****階、上**階**或****自我、下階、後**階**或自我（//）**、後面接著 **-同輩**、 **namespace**、**前面、****上-同輩**|  
|數值述詞||  
|算術運算子|mod|  
|節點函數|**上****階、上**階**或****自我、下階、後**階**或自我（//）**、後面接著 **-同輩**、 **namespace**、**前面、****上-同輩**|  
|字串函數|**string （）**、 **concat （）**、**開頭為（）**、**包含（）**、 **substring-before （）**、 **substring-after （）**、 **substring （**）、**字串長度（**）、正規化 **（）**、**轉譯（）**|  
|布林函數|**lang （）**|  
|數值函式|**sum （）**、 **floor （）**、**上限（）**、 **round （）**|  
|Union 運算子|&#124;|  
  
 當您在範本中指定 XPath 查詢時，請注意下列行為：  
  
-   XPath 可以包含在 XML 中具有特殊意義的字元，例如 < 或 & （範本是 XML 檔）。 您必須使用 XML & 編碼來將這些字元轉義，或在 URL 中指定 XPath。  
  
## <a name="see-also"></a>另請參閱  
 [在 SQLXML 4.0 中使用 XPath 查詢](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
