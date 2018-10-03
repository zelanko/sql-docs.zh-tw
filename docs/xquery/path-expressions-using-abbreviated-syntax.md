---
title: 使用縮寫語法中的路徑運算式 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7454eb815faf26248b4326487a833f0038f64c1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698266"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>路徑運算式 - 使用縮寫語法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  中的所有範例[了解 XQuery 中的路徑運算式](../xquery/path-expressions-xquery.md)使用路徑運算式的不縮寫的語法。 在路徑運算式中軸步的不縮寫語法包含軸名稱與節點測試，並以雙冒號分隔，後面接著零步或多步的限定詞。  
  
 例如：  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery 支援在路徑運算式中使用下列縮寫：  
  
-   **子系**軸是預設軸。 因此，**子系::** 軸可以從運算式中的步驟中省略。 例如，`/child::ProductDescription/child::Summary` 可以撰寫成 `/ProductDescription/Summary`。  
  
-   **屬性**軸可以縮寫成@。 例如，`/child::ProductDescription[attribute::ProductModelID=10]` 可以撰寫成 `/ProudctDescription[@ProductModelID=10]`。  
  
-   A **descendant-or-self::node()/** 可以縮寫成 / /。 例如，`/descendant-or-self::node()/child::act:telephoneNumber` 可以撰寫成 `//act:telephoneNumber`。  
  
     上一個查詢擷取了所有儲存在 Contact 資料表中 AdditionalContactInfo 資料行的電話號碼。 AdditionalContactInfo 的結構描述定義的方式， \<telephoneNumber > 項目可以出現在任何位置的文件。 因此，若要擷取所有的電話號碼，您必須搜尋文件中的每個節點。 將會從文件的根節點開始搜尋，並繼續搜尋所有的下階節點。  
  
     下列查詢會擷取特定客戶連絡人的所有電話號碼。  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="http://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     如果您以縮寫語法 `//act:telephoneNumber` 取代路徑運算式，您會收到相同的結果。  
  
-   **Self:: node （)** 在步驟中可以縮寫成單點 （.）。 不過，點不相等或使用可互換**self:: node （)**。  
  
     例如，在下列查詢中，點的使用代表是一個值且不是節點：  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   **父代:: node （)** 在步驟中可以縮寫成雙點 （.）。  
  
  
