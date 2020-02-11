---
title: UPDATE、DELETE 和 INSERT 語句 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942831"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 以及 INSERT 陳述式
以 SQL 為基礎的應用程式會藉由執行**UPDATE**、 **DELETE**和**INSERT**語句來對資料表進行變更。 這些語句是最低 SQL 文法一致性層級的一部分，而且必須受到所有驅動程式和資料來源的支援。  
  
 這些語句的語法如下：  
  
 **更新**_資料表-名稱_  
  
 **設定**資料_行識別碼_ **=** {*expression* &#124; **Null**}  
  
 [**，** 資料_行識別碼_ **=** {*expression* &#124; **Null**}] .。。  
  
 [**WHERE** _搜尋條件_]  
  
 **從**_資料表名稱_[**WHERE** _搜尋-條件_] 刪除  
  
 **插入**_資料表名稱_[（資料**** _行識別碼_[，資料**** _行識別碼_] .。。**)**]  
  
 {*查詢規格*&#124;**值（** _插入-值_[**，** _插入值_] .。。**)**}  
  
 請注意，*查詢規格*元素僅適用于 Core 和 extended sql 文法，而且*運算式*和*搜尋條件*元素在核心和擴充 sql 文法中會變得更複雜。  
  
 如同其他 SQL 語句， **UPDATE**、 **DELETE**和**INSERT**語句在使用參數時，通常會更有效率。 例如，您可以準備並重複執行下列語句，以便在 Orders 資料表中插入多個資料列：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 藉由傳遞參數值的陣列，可以增加這項效率。 如需有關語句參數和參數值陣列的詳細資訊，請參閱[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
