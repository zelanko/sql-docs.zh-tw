---
title: SELECT 陳述式的限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26bf17596dbd3279498df2edcee7636db95ae139
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127857"
---
# <a name="select-statement-limitations"></a>SELECT 陳述式限制
彙總函式資料行不能混合具有非彙總資料行的 SELECT 陳述式。  
  
 中有 GROUP BY 子句的 SELECT 陳述式的選取清單只能有 GROUP BY 子句中的運算式或集合函數。  
  
 不支援以星號 （選取所有資料行） 包含 GROUP BY 子句的 SELECT 陳述式中使用。 必須指定要選取的資料行的名稱。  
  
 不支援垂直列在 SELECT 陳述式中使用。 如果您需要參考到包含直條的資料值，請使用 SELECT 陳述式中的參數。  
  
 當 SELECT 陳述式中使用的資料行別名，"as"這個字必須在前面的別名。 例如，"做為 SELECT col1 b。 」 不含"於"陳述式會傳回錯誤。  
  
 如果 SELECT 陳述式輸入了不正確的資料行名稱，則 SQLSTATE 07001，「 錯誤號碼的參數，"會傳回錯誤而非 SQLSTATE S0022 錯誤，「 資料行找不到。 」  
  
 使用 Microsoft Excel 驅動程式時，如果空字串插入資料行，則為空字串會轉換成 null 值;搜尋的 SELECT 陳述式，會用 WHERE 子句中的空字串執行在該資料行，將會失敗。
