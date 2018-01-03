---
title: "SELECT 陳述式的限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08a26976ff3c71f604091b5b70fc37662ab2aea7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="select-statement-limitations"></a>SELECT 陳述式的限制
無法混合的彙總函式的資料行具有非彙總資料行中的 SELECT 陳述式。  
  
 有 GROUP BY 子句的 SELECT 陳述式的選取清單只能有 GROUP BY 子句中的運算式或設定函式。  
  
 不支援使用星號 （以選取所有資料行） 中包含 GROUP BY 子句的 SELECT 陳述式。 您必須指定要選取的資料行名稱。  
  
 不支援的垂直列在 SELECT 陳述式中使用。 如果您需要參考到包含直條的資料值，請使用 SELECT 陳述式中的參數。  
  
 當 SELECT 陳述式中使用的資料行別名，"as"這個字必須在前面的別名。 例如，"做為 SELECT col1 從 b。 」 不含"於"陳述式會傳回錯誤。  
  
 如果輸入了不正確的資料行名稱是 SELECT 陳述式，將 SQLSTATE 07001，「 錯誤數目的參數，"會傳回錯誤而 SQLSTATE S0022 錯誤，「 資料行找不到。 」  
  
 使用 Microsoft Excel 驅動程式時，如果空字串插入資料行，則為空字串會轉換成 null 值;搜尋 SELECT 陳述式執行時以空字串的 WHERE 子句中該資料行上，將會失敗。
