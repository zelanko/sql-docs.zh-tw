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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069974"
---
# <a name="using-the-odbc-cursor-library"></a>使用 ODBC 資料指標程式庫
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 若要使用 ODBC 資料指標程式庫，應用程式：  
  
1.  使用 SQL_ATTR_ODBC_CURSORS 的*屬性*呼叫**SQLSetConnectAttr** ，以指定資料指標程式庫應該如何與特定連接搭配使用。 資料指標程式庫可以一律使用（SQL_CUR_USE_ODBC），只有在驅動程式不支援可滾動的資料指標（SQL_CUR_USE_IF_NEEDED），或從未使用過（SQL_CUR_USE_DRIVER）時才使用。  
  
2.  呼叫**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**以連接到資料來源。  
  
3.  呼叫**SQLSetStmtAttr**來指定資料指標類型（SQL_ATTR_CURSOR_TYPE）、平行存取（SQL_ATTR_CONCURRENCY）和資料列集大小（SQL_ATTR_ROW_ARRAY_SIZE）。 資料指標程式庫支援順向和靜態資料指標。 順向資料指標必須是唯讀的，靜態資料指標可以是唯讀的，或可以使用開放式並行存取控制比較值。  
  
4.  配置一或多個資料列集緩衝區，並呼叫**SQLBindCol**一次或多次，以將這些緩衝區系結至結果集資料行。  
  
5.  藉由執行**SELECT**語句或程式，或藉由呼叫目錄函數來產生結果集。 如果應用程式將執行定位 update 語句，則應該執行**SELECT FOR update**語句來產生結果集。  
  
6.  呼叫**SQLFetch**或**SQLFetchScroll**一次或多次，以流覽結果集。  
  
 應用程式可以變更資料列集緩衝區中的資料值。 若要使用資料指標程式庫快取中的資料來重新整理資料列集緩衝區，應用程式會呼叫**SQLFetchScroll** ，並將*FetchOrientation*引數設為 SQL_FETCH_RELATIVE，並將*FetchOffset*引數設定為0。  
  
 若要從未系結的資料行抓取資料，應用程式會呼叫**SQLSetPos** ，將游標放在所需的資料列上。 然後，它會呼叫**SQLGetData**來取得資料。  
  
 為了判斷已從資料來源中取得的資料列數目，應用程式會呼叫**SQLRowCount**。
