---
title: 使用 ODBC 游標庫 ( 1) ( 1)微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c740ed78de51684eac38ad0c54ab2224986018d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301399"
---
# <a name="using-the-odbc-cursor-library"></a>使用 ODBC 資料指標程式庫
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 要使用 ODBC 游標庫應用程式:  
  
1.  使用SQL_ATTR_ODBC_CURSORS*屬性*調用**SQLSetConnectAttr,** 以指定如何將游標庫與特定連接一起使用。 游標庫始終可以使用(SQL_CUR_USE_ODBC),僅當驅動程式不支援可滾動的游標(SQL_CUR_USE_IF_NEEDED)或從未使用過(SQL_CUR_USE_DRIVER)時才使用。  
  
2.  調用**SQLConnect** **、SQLDriverConnect**或**SQLBrowse Connect**以連接到資料來源。  
  
3.  調用**SQLSetStmtAttr**指定游標類型(SQL_ATTR_CURSOR_TYPE)、併發(SQL_ATTR_CONCURRENCY)和行集大小(SQL_ATTR_ROW_ARRAY_SIZE)。 游標庫支援僅轉發和靜態游標。 僅轉發遊標必須是唯讀的,而靜態游標可以是唯讀的,或者可以使用樂觀併發控件比較值。  
  
4.  分配一個或多個行集緩衝區,並調用**SQLBindCol**一次或多次將這些緩衝區綁定到結果集列。  
  
5.  通過執行**SELECT**語句或過程或調用目錄函數生成結果集。 如果應用程式將執行定位更新語句,則應執行 **「選擇更新**」語句以生成結果集。  
  
6.  調用**SQLFetch**或**SQLFetch 滾動**一次或多次以滾動瀏覽結果集。  
  
 應用程式可以更改行集緩衝區中的數據值。 要使用游標庫緩存中的數據刷新行集緩衝區,應用程式將**SQLFetchScroll 調用 SQLFetchScroll,** 其中*Fetch 定向*參數設置為SQL_FETCH_RELATIVE,FetchOffset 參數設置為 0。 *FetchOffset*  
  
 若要從未綁定列檢索數據,應用程式將調用**SQLSetPos**將游標定位到所需的行上。 然後調用**SQLGetData**來檢索數據。  
  
 若要確定從資料來源索的行數,應用程式將呼叫**SQLRowCount**。
