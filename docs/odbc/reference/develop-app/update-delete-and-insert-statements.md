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
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942831"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 以及 INSERT 陳述式
以 SQL 為基礎的應用程式對資料表進行變更，藉由執行**更新**，**刪除**，並**插入**陳述式。 這些陳述式屬於 Minimum SQL 文法的一致性層級，而且必須支援的所有驅動程式和資料來源。  
  
 這些陳述式的語法是：  
  
 **更新** _資料表名稱_  
  
 **設定** _資料行識別碼_  **=** {*運算式* &#124; **NULL**}  
  
 [ **，** _資料行識別碼_  **=** {*運算式* &#124; **NULL**}]...  
  
 [**何處** _搜尋條件_]  
  
 **DELETE FROM** _table-name_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _資料表名稱_[ **(** _資料行識別碼_[ **，** _資料行識別碼_]... **)** ]  
  
 {*查詢規格* &#124; **值 (** _插入值_[ **，** _插入值_]... **)** }  
  
 請注意，*查詢規格*項目是只有在核心和 Extended SQL 文法，而且有效*運算式*並*搜尋條件*項目變得更複雜的核心和 Extended SQL 文法。  
  
 像其他 SQL 陳述式中，**更新**，**刪除**，和**插入**陳述式通常會更有效率使用參數時。 例如，下列陳述式可以備妥，並重複執行，以將多個資料列插入 Orders 資料表中：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 這種效率可以增加所傳遞的參數值的陣列。 如需有關陳述式參數和參數值的陣列的詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。
