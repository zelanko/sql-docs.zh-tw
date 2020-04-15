---
title: 更新、刪除和插入語句 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f12682a5d012d6981afce0085e9c920ed2f2ffbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284258"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 以及 INSERT 陳述式
基於 SQL 的應用程式執行**更新**、**刪除**和**INSERT**語句對表進行更改。 這些語句是最小 SQL 語法一致性級別的一部分,必須得到所有驅動程序和數據源的支援。  
  
 這些語句的語法是:  
  
 **更新**_表格名稱_  
  
 **設定**_欄識別碼_**=**= &#124; **NULL**的*表示式*|  
  
 【**,**_列識別子_**=**】*表示式*&#124; **NULL**_...  
  
 【**WHERE** _搜尋條件_】  
  
 **從**_表名中移除_[**WHERE** _搜尋條件_]  
  
 **插入表**_名_=**(**_列識別子_=**,** _欄識別子_* ...**)**]  
  
 【*查詢規範*&#124;**值 (**_插入值_#**,** _插入值_# ...**)**}  
  
 請注意,*查詢規範*元素僅在核心和擴展 SQL 語法中有效,並且*運算式*和*搜尋條件*元素在核心和擴展 SQL 語法中變得更加複雜。  
  
 與其他 SQL 語句一樣,**更新**、**刪除**和**INSERT**語句在使用參數時通常更有效率。 例如,可以準備並重複執行以下語句,以在「訂單」表中插入多行:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 通過傳遞參數值數組可以提高這種效率。 有關敘述參數與參數值陣列的詳細資訊,請參閱[敘述參數](../../../odbc/reference/develop-app/statement-parameters.md)。
