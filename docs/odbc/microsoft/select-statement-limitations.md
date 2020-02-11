---
title: SELECT 語句限制 |Microsoft Docs
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
ms.openlocfilehash: 0cde0158e72d1e24c112c8e7955f0d6b317bd729
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987857"
---
# <a name="select-statement-limitations"></a>SELECT 陳述式限制
彙總函式資料行不能與 SELECT 語句中的非匯總資料行混合使用。  
  
 具有 GROUP BY 子句的 SELECT 語句之選取清單，只能有 GROUP BY 子句中的運算式或設定函數。  
  
 不支援在包含 GROUP BY 子句的 SELECT 語句中使用星號（以選取所有資料行）。 必須指定要選取之資料行的名稱。  
  
 不支援在 SELECT 語句中使用分隔號。 如果您需要參考包含分隔號的資料值，請在 SELECT 語句中使用參數。  
  
 在 SELECT 語句中使用資料行別名時，"as" 這個字必須在別名前面。 例如，「SELECT col1 as a from b」。 如果沒有 "as"，語句會傳回錯誤。  
  
 如果在 SELECT 語句中輸入不正確的資料行名稱，則會傳回 SQLSTATE 07001 錯誤「參數數目錯誤」，而不是 SQLSTATE S0022 錯誤「找不到資料行」。  
  
 使用 Microsoft Excel 驅動程式時，如果將空字串插入至資料行，則會將空字串轉換成 Null;在 WHERE 子句中使用空字串執行的搜尋 SELECT 語句將不會在該資料行上成功。
