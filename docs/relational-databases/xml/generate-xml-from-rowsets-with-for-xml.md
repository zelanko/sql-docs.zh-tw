---
title: 使用 FOR XML 從資料列集產生 XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b1555b97b1d6f31c8d7aef6b002e1c9f05c976be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856506"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>使用 FOR XML 從資料列集產生 XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  您可以使用 FOR XML 搭配新的 **TYPE** 指示詞，以從資料列集產生 **xml** 資料類型執行個體。  
  
 其結果可以指派給 **xml** 資料類型資料行、變數或參數。 此外，還可以將 FOR XML 巢狀化，以產生任何階層式結構。 與 FOR XML EXPLICIT 相較，這樣撰寫巢狀 FOR XML 更為方便，但是對於較深的階層，其效能可能沒那麼好。 FOR XML 也導入了一種新的 PATH 模式。 這種新模式可以在資料行值出現的 XML 樹狀結構中指定路徑。  
  
 新的 **FOR XML TYPE** 指示詞可用來定義含有 SQL 語法之關聯式資料的唯讀 XML 檢視。 您可以用 SQL 陳述式和內嵌的 XQuery 來查詢該檢視，如下列範例所示。 您也可以在預存程序中參照這些 SQL 檢視。  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>範例：傳回所產生之 xml 資料類型的 SQL 檢視  
 下列 SQL 檢視定義會建立一個 XML 檢視，可供檢視從 XML 資料行中擷取的關聯式資料行、pk 及書籍作者。  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 V 檢視包含單一資料列及 XML 類型的單一 columnxmlVal`.` 。其查詢方法就像一般 **xml** 資料類型執行個體一樣。 例如，下列查詢會傳回名字叫 "David" 的作者：  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 SQL 檢視定義有點像用註解結構描述來建立的 XML 檢視。 但是，有幾個重要的相異之處。 SQL 檢視定義是唯讀的，而且必須用內嵌的 XQuery 來操控。 XML 檢視則是用註解結構描述所建立。 此外，SQL 檢視會先將 XML 結果具體化，再套用 XQuery 運算式，而 XML 檢視上的 XPath 查詢則是會在基礎資料表上評估 SQL 查詢。  
  
## <a name="see-also"></a>另請參閱  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
