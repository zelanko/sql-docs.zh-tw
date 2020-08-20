---
description: UPDATE、DELETE 以及 INSERT 陳述式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b01582594bb54f8feafef3f98118d3e17286fae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487421"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 以及 INSERT 陳述式
以 SQL 為基礎的應用程式會藉由執行 **UPDATE**、 **DELETE**和 **INSERT** 語句來變更資料表。 這些語句是最基本的 SQL 文法一致性層級的一部分，而且必須由所有驅動程式和資料來源支援。  
  
 這些語句的語法如下：  
  
 **更新**_資料表名稱_  
  
 **設定**資料 _行識別碼_ **=** {*expression* &#124; **Null**}  
  
 [**，** 資料 _行識別碼_ **=** {*expression* &#124; **Null**}]...  
  
 [**WHERE** _搜尋條件_]  
  
 **從**_資料表名稱_刪除 [**WHERE** _搜尋條件_]  
  
 **插入**_資料表名稱_[ (資料** (** _行識別碼_[，資料 **,** _行識別碼_] .。。**) **]  
  
 {*查詢規格* &#124; **值 (** _插入值_ [**，** _插入值_] .。。**) **}  
  
 請注意， *查詢規格* 元素只適用于 Core 和擴充的 sql 文法，而且在核心和擴充的 sql 文法中， *運算式* 和 *搜尋條件* 元素會變得更複雜。  
  
 如同其他 SQL 語句， **UPDATE**、 **DELETE**和 **INSERT** 語句在使用參數時，通常會更有效率。 例如，下列語句可以備妥並重複執行，以便在 Orders 資料表中插入多個資料列：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 您可以傳遞參數值陣列來提高這項效率。 如需有關語句參數和參數值陣列的詳細資訊，請參閱 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
