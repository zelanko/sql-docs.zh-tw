---
title: 預設 C 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307049"
---
# <a name="default-c-data-types"></a>預設 C 資料類型
如果應用程式在**SQLBindCol**、 **SQLGetData**或**SQLBindParameter**中指定 SQL_C_DEFAULT，則驅動程式會假設輸出或輸入緩衝區的 C 資料類型對應到緩衝區所系結之資料行或參數的 SQL 資料類型。  
  
> [!IMPORTANT]  
>  互通的應用程式不應該使用 SQL_C_DEFAULT。 相反地，它們應該一律指定所使用之緩衝區的 C 類型。 這是因為因為下列原因，驅動程式無法一律正確判斷預設 C 類型：  
  
-   如果 DBMS 升級資料行或參數的 SQL 資料類型，則驅動程式無法判斷資料行或參數的原始 SQL 資料類型。 因此，它無法判斷對應的預設 C 資料類型。  
  
-   如果驅動程式無法判斷特定的資料行或參數是否已簽署，通常是由 DBMS 處理這種情況，驅動程式就無法判斷對應的預設 C 資料類型是否應該簽署或不帶正負號。  
  
     因為 SQL_C_DEFAULT 只是為了方便程式設計而提供，所以當它指定實際的 C 資料類型時，並不會遺失任何功能。  
  
 針對每個 SQL 資料類型顯示預設 C 資料類型的資料表，會包含在本附錄稍後的將[資料從 Sql 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。
