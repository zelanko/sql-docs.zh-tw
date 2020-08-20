---
description: SQLFetchScroll (資料指標程式庫)
title: SQLFetchScroll (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9783e2e0e7e5030aef0173a67cf8a4eac416242f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461650"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLFetchScroll** 函數。 如需 **SQLFetchScroll**的一般資訊，請參閱 [SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 資料指標程式庫會在驅動程式中重複呼叫**SQLFetch** ，以執行**SQLFetchScroll** 。 它會將它從驅動程式取出的資料傳輸至應用程式所提供的資料列集緩衝區。 它也會將資料快取在記憶體和磁片檔案中。 當應用程式要求新的資料列集時，資料指標程式庫會視需要從驅動程式進行抓取 (如果先前尚未提取) 或快取 (（如果先前已取得) ）。 最後，資料指標程式庫會維護快取資料的狀態，並將這項資訊傳回至資料列狀態陣列中的應用程式。  
  
 使用資料指標程式庫時，對 **SQLFetchScroll** 的呼叫不能與 **SQLFetch** 或 **SQLExtendedFetch**的呼叫混合。  
  
 使用資料指標程式庫時，ODBC 2 同時支援對 **SQLFetchScroll** 的呼叫。*x* 和 for ODBC 3。*x* 驅動程式。  
  
## <a name="rowset-buffers"></a>資料列集緩衝區  
 資料指標程式庫會將從驅動程式傳送至應用程式所提供之資料列集緩衝區的資料優化（如果：  
  
-   應用程式會使用資料列取向的系結。  
  
-   應用程式在結構中的欄位之間沒有未使用的位元組，以保存資料列。  
  
-   **SQLFetch**或**SQLFetchScroll**傳回資料行之長度/指標的欄位，會遵循該資料行的緩衝區，並在下一個資料行的緩衝區之前。 這些欄位為選擇性。  
  
 當應用程式要求新的資料列集時，資料指標程式庫會視需要從其快取和驅動程式抓取資料。 如果新的和舊的資料列集重迭，則資料指標程式庫可以重複使用資料列集緩衝區之重迭區段的資料，以優化其效能。 因此，除非新的和舊的資料列集重迭，而且變更是在資料列集緩衝區的重迭區段中，否則資料列集緩衝區的未儲存變更將會遺失。 若要儲存變更，應用程式會提交定位的 update 語句。  
  
 請注意，當應用程式呼叫 **SQLFetchScroll** 時，資料指標程式庫一律會使用快取中的資料來重新整理資料列集緩衝區，並將 *FetchOrientation* 引數設定為 SQL_FETCH_RELATIVE，並將 *FetchOffset* 引數設定為0。  
  
 資料指標程式庫支援使用 SQL_ATTR_ROW_ARRAY_SIZE 的*屬性*來呼叫**SQLSetStmtAttr** ，以便在資料指標開啟時變更資料列集大小。 新的資料列集大小會在下次呼叫 **SQLFetchScroll** 時生效。  
  
## <a name="result-set-membership"></a>結果集成員資格  
 資料指標程式庫只會在應用程式要求時，從驅動程式抓取資料。 視資料來源和 SQL_CONCURRENCY 語句屬性的設定而定，這會產生下列結果：  
  
-   資料指標程式庫所抓取的資料可能與執行語句時可用的資料不同。 例如，在開啟資料指標之後，插入資料列的資料列可能會由某些驅動程式抓取。  
  
-   資料指標程式庫的資料來源可能會鎖定結果集內的資料，因此其他使用者無法使用。  
  
 當資料指標程式庫快取了資料列之後，它就無法偵測到基礎資料來源中該資料列的變更 (但在相同資料指標的快取) 上操作的是定點更新和刪除作業。 發生這種情況是因為呼叫 **SQLFetchScroll**時，資料指標程式庫永遠不會 refetches 資料來源中的資料。 相反地，它會從其快取中 refetches 資料。  
  
## <a name="scrolling"></a>捲動  
 資料指標程式庫支援在 **SQLFetchScroll**中執行下列提取類型。  
  
|資料指標類型|提取類型|  
|-----------------|-----------------|  
|順向|SQL_FETCH_NEXT|  
|靜態|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 當呼叫 **SQLFetchScroll** ，且其中一個 **SQLFetch** 呼叫傳回 SQL_ERROR 時，資料指標程式庫會依照下列方式繼續進行。 完成這些步驟之後，資料指標程式庫會繼續處理。  
  
1.  呼叫 **SQLGetDiagRec** 以從驅動程式取得錯誤資訊，並將其張貼為驅動程式管理員中的診斷記錄。  
  
2.  將診斷記錄中的 SQL_DIAG_ROW_NUMBER 欄位設定為適當的值。  
  
3.  將診斷記錄中的 SQL_DIAG_COLUMN_NUMBER 欄位設定為適當的值（如果適用）。否則，它會將它設定為0。  
  
4.  設定資料列狀態陣列中錯誤資料列的值，以 SQL_ROW_ERROR。  
  
 當資料指標程式庫在其**SQLFetchScroll**的執行中多次呼叫**SQLFetch**時，其中一個**SQLFetch**的呼叫所傳回的任何錯誤或警告都會在診斷記錄中，而且可以藉由呼叫**SQLGetDiagRec**來取出。 如果資料在提取時遭到截斷，截斷的資料現在將會位於資料指標程式庫的快取中。 後續呼叫 **SQLFetchScroll** 以滾動至具有截斷資料的資料列，將會傳回截斷的資料，而且不會引發任何警告，因為資料會從資料指標程式庫的快取中提取。 若要追蹤傳回的資料長度，以便能夠判斷緩衝區中傳回的資料是否已遭截斷，應用程式應該系結長度/指標緩衝區。  
  
## <a name="bookmark-operations"></a>書簽作業  
 資料指標程式庫支援使用*FetchOrientation*的 SQL_FETCH_BOOKMARK 來呼叫**SQLFetchScroll** 。 它也支援在 *FetchOffset* 引數中指定可在書簽作業中使用的位移。 這是資料指標程式庫唯一支援的書簽作業。 資料指標程式庫不支援呼叫 **SQLBulkOperations**。  
  
 如果應用程式已設定 SQL_ATTR_USE_BOOKMARKS 語句屬性，且已系結至書簽資料行，則資料指標程式庫會產生固定長度的書簽，並將其傳回給應用程式。 資料指標程式庫會建立和維護其所使用的書簽;它不會使用在資料來源中維護的書簽。 當呼叫 **SQLFetchScroll** 來取出已經從資料來源提取的資料區塊時，它會從資料指標程式庫快取中抓取資料。 如此一來，在 SQL_FETCH_BOOKMARK **SQLFetchScroll** 的呼叫中 *所使用的* 書簽必須由資料指標程式庫建立和維護。  
  
## <a name="interaction-with-other-functions"></a>與其他函式互動  
 應用程式必須先呼叫 **SQLFetch** 或 **SQLFetchScroll** ，才能準備或執行任何定位的 update 或 delete 語句。
