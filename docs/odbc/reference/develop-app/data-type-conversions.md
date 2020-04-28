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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305210"
---
# <a name="data-type-conversions"></a>資料類型轉換
資料可以從一種類型轉換成另一種類型：當資料從某個應用程式變數傳輸到另一個（C 到 C）時，當應用程式變數中的資料傳送至語句參數（C 到 SQL）時，如果結果集資料行中的資料是在應用程式變數（SQL 到 C）中傳回，且資料從某個資料來源資料行傳送到另一個（SQL 到 SQL）時。  
  
 當資料從某個應用程式變數轉移到另一個時所發生的任何轉換，都不在本檔的討論範圍內。  
  
 當應用程式將變數系結至結果集資料行或語句參數時，應用程式會以隱含方式在其選擇的應用程式變數資料類型中指定資料類型轉換。 例如，假設資料行包含整數資料。 如果應用程式將整數變數系結至資料行，則會指定不進行轉換。如果應用程式將字元變數系結至資料行，它會指定要從整數轉換成字元。  
  
 ODBC 會定義在每個 SQL 和 C 資料類型之間轉換資料的方式。 基本上，ODBC 支援所有合理的轉換，例如字元到整數和整數到 float，而且不支援錯誤定義的轉換，例如 float to date。 需要驅動程式才能支援每個支援的 SQL 資料類型的所有轉換。 如需 SQL 和 C 資料類型之間轉換的完整清單，請參閱附錄 D：資料類型中的將[資料從 Sql 轉換成 c 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)和[將資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
 ODBC 也會定義純量函數，以便將資料從一個 SQL 資料類型轉換成另一個。 **轉換**純量函數會由驅動程式對應到基礎純量函數，或定義為在資料來源中執行轉換的函數。 因為此函式會對應至 DBMS 特有的函數，所以 ODBC 不會定義這些轉換的運作方式，或是必須支援的轉換。 應用程式會透過**SQLGetInfo**中的 SQL_CONVERT 選項，探索特定驅動程式和資料來源所支援的轉換。 如需**CONVERT**純量函數的詳細資訊，請參閱[ODBC 中的 Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[明確的資料類型轉換函](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)式。
