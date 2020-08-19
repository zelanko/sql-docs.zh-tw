---
description: 資料類型轉換
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
ms.openlocfilehash: 92c31cb12c7bb02cf8e108251ae5ebd6f12aed5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429340"
---
# <a name="data-type-conversions"></a>資料類型轉換
您可以將資料從一種類型轉換成另一種類型（四次）：當資料從某個應用程式變數傳送到另一個應用程式變數到另一個應用程式變數時，如果將應用程式變數中的資料傳送至 sql) )  (的語句參數，則會將該資料從一個應用程式變數傳送至 sql 時，結果 (集資料行中的資料會在應用程式變數中傳回 (SQL 到 C) ，以及將資料從某個資料  
  
 當資料從某個應用程式變數傳送到另一個應用程式變數時，所發生的任何轉換都不在本檔的討論範圍內。  
  
 當應用程式將變數系結至結果集資料行或語句參數時，應用程式會隱含地將資料類型轉換指定為應用程式變數的資料類型選擇。 例如，假設資料行包含整數資料。 如果應用程式將整數變數系結至資料行，則會指定不執行任何轉換;如果應用程式將字元變數系結至資料行，它會指定將資料從整數轉換成字元。  
  
 ODBC 會定義在每個 SQL 和 C 資料類型之間轉換資料的方式。 基本上，ODBC 支援所有合理的轉換，例如將字元轉換為整數，並將整數轉換為浮點數，而且不支援錯誤定義的轉換，例如 float 至今的轉換。 需要驅動程式，才能支援所支援之每個 SQL 資料類型的所有轉換。 如需 SQL 與 C 資料類型之間轉換的完整清單，請參閱附錄 D：資料類型中的將 [資料從 Sql 轉換成 c 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) ，以及 [將資料從 c 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 。  
  
 ODBC 也會定義純量函數，以便將資料從一個 SQL 資料類型轉換成另一個。 **CONVERT**純量函數會由驅動程式對應到基礎純量函數，或定義為在資料來源中執行轉換的函數。 因為此函式對應至 DBMS 特定的函式，所以 ODBC 不會定義這些轉換的運作方式或必須支援的轉換。 應用程式會透過 **SQLGetInfo**中的 SQL_CONVERT 選項，探索特定驅動程式和資料來源所支援的轉換。 如需 **CONVERT** 純量函數的詳細資訊，請參閱 [ODBC 中的 Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 和 [明確的資料類型轉換函](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)式。
