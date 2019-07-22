---
title: 使用 FOR XML 的 RAW 模式 | Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac5e5ccf60594d41ff89d9ef5bd2c4342944a6da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016155"
---
# <a name="use-raw-mode-with-for-xml"></a>搭配 FOR XML 使用 RAW 模式

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

RAW 模式會將查詢結果集的每一個資料列轉換成具有泛用識別碼 \<資料列> 的 XML 項目，或選擇性提供的項目名稱。 依預設，資料列集內每一個非 NULL 的資料行值，都會對應到一個 \<資料列> 項目的屬性。 若將 ELEMENTS 指示詞加入 FOR XML 子句，則每一個資料行值都會對應到一個 \<資料列> 項目的子項目。 您還可以搭配 ELEMENTS 指示詞，選擇性地指定 XSINIL 選項，將結果集的 NULL 資料行值對應到具有 `xsi:nil="true"` 屬性的項目。
  
 您可以要求結果 XML 傳回結構描述。 指定 XMLDATA 選項可傳回內嵌 XDR 結構描述。 指定 XMLSCHEMA 選項則可傳回內嵌 XSD 結構描述。 結構描述會出現在資料的開頭。 在結果中，結構描述命名空間參考會在每個最上層的元素重複出現。  
  
 FOR XML 子句中必須指定 BINARY BASE64 選項，才能以 Base64 編碼格式傳回二進位資料。 在 RAW 模式中，若未指定 BINARY BASE64 選項，則擷取二進位資料就會發生錯誤。  
  
## <a name="in-this-section"></a>本節內容  
 本節包含下列範例：  
  
-   [範例：以 XML 的形式擷取產品型號資訊](../../relational-databases/xml/example-retrieving-product-model-information-as-xml.md)  
  
-   [範例：使用 ELEMENTS 指示詞指定 XSINIL](../../relational-databases/xml/example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [範例：使用 XMLDATA 和 XMLSCHEMA 選項要求結構描述的結果](../../relational-databases/xml/example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [範例：擷取二進位資料](../../relational-databases/xml/example-retrieving-binary-data.md)  
  
-   [範例：重新命名 &#60;row&#62; 元素](../../relational-databases/xml/example-renaming-the-row-element.md)  
  
-   [範例：為 FOR XML 產生的 XML 指定根元素](../../relational-databases/xml/example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [範例：查詢 XMLType 資料行](../../relational-databases/xml/example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [搭配 FOR XML 使用 AUTO 模式](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 EXPLICIT 模式](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)
  
  
