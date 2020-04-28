---
title: SQLGetData （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307839"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLGetData**函數。 如需有關**SQLGetData**的一般資訊，請參閱[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 資料指標程式庫會先使用**WHERE**子句來建立**SELECT**語句，以列舉在目前資料列中每個系結資料行的快取中儲存的值，藉以執行**SQLGetData** 。 然後，它會執行**SELECT**語句來重新選取資料列，並呼叫驅動程式中的**SQLGetData** ，以從資料來源（而不是快取）抓取資料。  
  
> [!CAUTION]  
>  用來識別目前資料列的資料指標程式庫所建立的**WHERE**子句，可能無法識別任何資料列、識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱[建立搜尋的語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE，可以在資料行0上呼叫**SQLGetData**以傳回書簽資料。  
  
 對**SQLGetData**的呼叫會受到下列限制：  
  
-   無法針對順向資料指標呼叫**SQLGetData** 。  
  
-   只有在符合下列條件時，才可以呼叫**SQLGetData** ： **SELECT**語句產生結果集;**SELECT**語句不包含 Join、 **UNION**子句或**GROUP BY**子句。而在選取清單中使用別名或運算式的任何資料行，都不會與**SQLBindCol**系結。  
  
-   如果驅動程式只支援一個作用中的語句，則資料指標程式庫會在執行**SELECT**語句並呼叫**SQLGetData**之前，先提取結果集的其餘部分。
