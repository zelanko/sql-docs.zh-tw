---
description: 預設 C 資料類型
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
ms.openlocfilehash: 7d0ed42971405ca23d5f69f47cbb6ac02e8e5675
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456604"
---
# <a name="default-c-data-types"></a>預設 C 資料類型
如果應用程式在 **SQLBindCol**、 **SQLGetData**或 **SQLBindParameter**中指定 SQL_C_DEFAULT，驅動程式會假設輸出或輸入緩衝區的 C 資料類型對應于緩衝區所系結之資料行或參數的 SQL 資料類型。  
  
> [!IMPORTANT]  
>  互通的應用程式不應該使用 SQL_C_DEFAULT。 相反地，它們應該一律指定所使用之緩衝區的 C 類型。 這是因為驅動程式無法一律正確地判斷預設的 C 類型，原因如下：  
  
-   如果 DBMS 升級的是資料行或參數的 SQL 資料類型，驅動程式就無法判斷資料行或參數的原始 SQL 資料類型。 因此，它無法判斷對應的預設 C 資料類型。  
  
-   如果驅動程式無法判斷特定的資料行或參數是否經過簽署，通常是 DBMS 處理這種情況時，驅動程式無法判斷對應的預設 C 資料類型是否應該簽署或不帶正負號。  
  
     由於 SQL_C_DEFAULT 僅為了程式設計方便而提供，因此當應用程式指定實際的 C 資料類型時，並不會遺失任何功能。  
  
 在此附錄稍後的將 [資料從 Sql 轉換成 c 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)時，會包含每個 sql 資料類型的預設 C 資料類型的資料表。
