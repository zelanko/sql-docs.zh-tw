---
title: 資料類型轉換 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305210"
---
# <a name="data-type-conversions"></a>資料類型轉換
數據可以在四次之一時從一種類型轉換為另一種類型:當數據從一個應用程式變數傳輸到另一個應用程式變數(C 到 C)、將應用程式變數中的數據發送到語句參數 (C 到 SQL)時、在應用程式變數(SQL 到 C)中返回結果集列中的數據時,以及數據從一個數據源列傳輸到另一個數據源列時(SQL 到 SQL)。  
  
 當數據從一個應用程式變數傳輸到另一個應用程式變數時發生的任何轉換都不在本文檔的範圍之內。  
  
 當應用程式將變數綁定到結果集列或語句參數時,應用程式隱式指定數據類型轉換,以選擇應用程式變數的數據類型。 例如,假設列包含整數數據。 如果應用程式將整數變數綁定到列,則指定不執行任何轉換;如果應用程式將整數變數變量綁定到列,則不執行任何轉換。如果應用程式將字元變數綁定到列,則指定將數據從整數轉換為字元。  
  
 ODBC 定義如何在每種 SQL 和 C 數據類型之間轉換數據。 基本上,ODBC 支援所有合理的轉換,例如字元到整數和整數到浮點,並且不支援定義不當的轉換,如浮動至今。 需要驅動程式來支援他們支援的每個 SQL 資料類型的所有轉換。 有關 SQL 與 C 資料型態之間的轉換的完整清單,請參考在附錄 D:資料型態中[將資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)以及[將資料從 C 轉換為 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
 ODBC 還定義了用於將數據從一種 SQL 資料類型轉換為另一種 SQL 資料類型的標量函數。 **CONVERT**標量函數由驅動程式映射到為在資料源中執行轉換而定義的基礎標量函數或函數。 由於此函數映射到特定於 DBMS 的函數,因此 ODBC 不定義這些轉換的工作原理或必須支援哪些轉換。 應用程式透過**SQLGetInfo**中的SQL_CONVERT選項發現特定驅動程式和數據來源支援哪些轉換。 有關**CONVERT**標量函數的詳細資訊,請參閱[ODBC 中的轉義序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)與[顯式資料類型轉換函數](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
