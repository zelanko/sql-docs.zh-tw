---
title: 使用 ODBC 資料指標程式庫 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdddf2e757c549de460f5e22c2ea76ce91a2a969
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069974"
---
# <a name="using-the-odbc-cursor-library"></a>使用 ODBC 資料指標程式庫
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 若要使用 ODBC 資料指標程式庫，應用程式：  
  
1.  呼叫**SQLSetConnectAttr**具有*屬性*的 SQL_ATTR_ODBC_CURSORS 來指定資料指標程式庫與特定連接的用法。 資料指標程式庫可以一律是 (SQL_CUR_USE_ODBC)，使用只有當驅動程式不支援可捲動資料指標 (SQL_CUR_USE_IF_NEEDED)，或從未使用過 (SQL_CUR_USE_DRIVER)。  
  
2.  呼叫**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**來連接到資料來源。  
  
3.  呼叫**SQLSetStmtAttr**指定資料指標類型 (SQL_ATTR_CURSOR_TYPE)、 並行存取 (SQL_ATTR_CONCURRENCY)，以及資料列集大小 (SQL_ATTR_ROW_ARRAY_SIZE)。 資料指標程式庫支援順向和靜態資料指標。 順向資料指標必須是唯讀的而靜態資料指標可以是唯讀或可使用 比較值的開放式並行存取控制。  
  
4.  配置一個或多個資料列集的緩衝區，以及呼叫**SQLBindCol**繫結至結果集資料行緩衝區的一或多次。  
  
5.  會產生結果集，藉由執行**選取**陳述式或程序，或呼叫目錄函數。 如果應用程式會執行定位的 update 陳述式，它應該執行**選取用於更新**陳述式來產生結果集。  
  
6.  呼叫**SQLFetch**或是**SQLFetchScroll**捲動的結果集的一或多次。  
  
 應用程式可以變更資料列集的緩衝區中的資料值。 若要重新整理的資料列集緩衝區，以從資料指標程式庫的快取的資料，應用程式會呼叫**SQLFetchScroll**具有*Sqlfetchscroll*引數設定為 sql_fetch_relative 但和*FetchOffset*引數設定為 0。  
  
 若要擷取的未繫結的資料行，應用程式會呼叫中的資料**SQLSetPos**若要將游標放在所需的資料列。 然後它會呼叫**SQLGetData**來擷取資料。  
  
 若要判斷資料來源中擷取的資料列數目，應用程式會呼叫**SQLRowCount**。
