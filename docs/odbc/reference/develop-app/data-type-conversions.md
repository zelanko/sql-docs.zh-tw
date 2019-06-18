---
title: 資料類型轉換 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84710ffd69ea377c979adf94af1394d8436ef10b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640473"
---
# <a name="data-type-conversions"></a>資料類型轉換
資料可從一種類型中轉換到另一個，在其中一個四次： 當資料傳輸從一個應用程式變數到另一個 (C 到 C)，當應用程式變數中的資料傳送至陳述式參數 (C 到 SQL) 中傳回結果集資料行中的資料時應用程式變數 (SQL 到 C) 和資料時從一個資料來源的資料行傳送至另一個 (SQL to SQL)。  
  
 當資料從一個應用程式變數傳送至另一個時，就會發生任何轉換已超出本文的範圍。  
  
 當應用程式會將變數繫結至結果集資料行或陳述式參數時，應用程式會隱含指定的資料類型轉換中選擇的應用程式變數的資料類型。 例如，假設資料行包含整數資料。 如果應用程式會將整數變數繫結至資料行，它就會指定不完成任何轉換;如果應用程式會將字元變數繫結至資料行，它會指定，資料會從整數轉換成字元。  
  
 ODBC 定義每個 SQL 和 C 資料類型之間轉換資料的方式。 基本上，ODBC 支援所有合理轉換的詳細資訊，例如整數和浮點數到整數的字元，而且不支援定義不正確的轉換，例如浮點數的日期。 支援每個 SQL 資料類型所支援的所有轉換所需驅動程式。 SQL 和 C 資料類型之間轉換的完整清單，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)並[轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附錄 d:資料類型。  
  
 ODBC 也會定義將資料從一個 SQL 資料類型轉換為另一個純量函數。 **轉換**純量函式所對應的驅動程式為基礎的純量函式來執行轉換的資料來源中定義的函式。 此函式會對應至特定 DBMS 的函式，因為這些轉換的運作方式，或必須支援何種轉換，不會定義 ODBC。 應用程式可讓您探索哪些轉換支援透過 SQL_CONVERT 選項的特定驅動程式和資料來源**SQLGetInfo**。 如需詳細資訊**轉換**純量函數，請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)並[明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
