---
title: 資料型別轉換 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04dd1614247067e3920958f9d1733a3ef91d792c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-conversions"></a>資料類型轉換
資料可以從一個類型中轉換到另一個，其中一個四次： 當資料傳送從一個應用程式變數到另一個 (C 到 C)，當應用程式變數中的資料傳送至陳述式參數 (C to SQL) 中傳回結果集資料行中的資料時應用程式變數 (SQL 到 C)，並將資料時從一個資料來源資料行轉移至另一個 (SQL to SQL)。  
  
 當資料從一個應用程式變數傳送至另一個時，就會發生任何轉換超出本文的範圍。  
  
 當應用程式會將變數繫結至結果集資料行或陳述式參數時，應用程式以隱含方式指定資料類型轉換中所選擇的應用程式變數的資料類型。 例如，假設資料行包含整數資料。 如果應用程式會將整數變數繫結至資料行，它會指定不完成任何轉換;如果應用程式會將字元變數繫結至資料行，它會指定從整數轉換資料，為字元。  
  
 ODBC 定義每個 SQL 和 C 資料類型之間轉換資料的方式。 基本上，ODBC 支援所有合理轉換的詳細資訊，例如整數和浮點數，到整數字元，並不支援定義不正確的轉換，例如浮點數的日期。 它們支援每個 SQL 資料類型支援的所有轉換所需的驅動程式。 SQL 和 C 資料類型之間轉換的完整清單，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)和[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附錄 d： 資料型別中。  
  
 ODBC 也已經定義的純量函式將資料從一個 SQL 資料類型轉換成另一個。 **轉換**純量函式由驅動程式新增至基準的純量函數或執行轉換資料來源中定義的函式對應。 此函式對應至 DBMS 特有的函式，因為這些轉換的運作方式，或必須支援何種轉換，不會定義 ODBC。 應用程式可讓您探索哪些轉換所支援特定的驅動程式和資料來源中的 SQL_CONVERT 選項透過**SQLGetInfo**。 如需有關**轉換**純量函數，請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
