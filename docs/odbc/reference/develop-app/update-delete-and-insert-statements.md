---
title: UPDATE、 DELETE 和 INSERT 陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00732de7eca32dc8b2984fdda14163c77c66ad43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632476"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 以及 INSERT 陳述式
以 SQL 為基礎的應用程式對資料表進行變更，藉由執行**更新**，**刪除**，並**插入**陳述式。 這些陳述式屬於 Minimum SQL 文法的一致性層級，而且必須支援的所有驅動程式和資料來源。  
  
 這些陳述式的語法是：  
  
 **更新** _資料表名稱_  
  
 **設定** _資料行識別碼_  **=** {*運算式* &#124; **NULL**}  
  
 [ **，** _資料行識別碼_  **=** {*運算式* &#124; **NULL**}]...  
  
 [**何處** _搜尋條件_]  
  
 **DELETE FROM** _table-name_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _table-name_[ **(** _column-identifier_ [ **,** _column-identifier_]... **)** ]  
  
 {*query-specification* &#124; **VALUES (** _insert-value_ [ **,** _insert-value_]... **)** }  
  
 請注意，*查詢規格*項目是只有在核心和 Extended SQL 文法，而且有效*運算式*並*搜尋條件*項目變得更複雜的核心和 Extended SQL 文法。  
  
 像其他 SQL 陳述式中，**更新**，**刪除**，和**插入**陳述式通常會更有效率使用參數時。 例如，下列陳述式可以備妥，並重複執行，以將多個資料列插入 Orders 資料表中：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 這種效率可以增加所傳遞的參數值的陣列。 如需有關陳述式參數和參數值的陣列的詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。
