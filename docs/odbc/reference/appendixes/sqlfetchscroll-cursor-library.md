---
title: SQLFetchScroll （資料指標程式庫） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16e7e4d133fdfafd7a005c19b0a2943b2ea9ef6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086447"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLFetchScroll**函數。 如需有關**SQLFetchScroll**的一般資訊，請參閱[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 資料指標程式庫會藉由重複呼叫驅動程式中的**SQLFetch**來執行**SQLFetchScroll** 。 它會將它從驅動程式抓取的資料傳輸到應用程式所提供的資料列集緩衝區。 它也會將資料快取到記憶體和磁片檔案中。 當應用程式要求新的資料列集時，資料指標程式庫會視需要從驅動程式（如果先前尚未提取）或快取（如果先前已提取）來抓取它。 最後，資料指標程式庫會維護快取資料的狀態，並將此資訊傳回資料列狀態陣列中的應用程式。  
  
 使用資料指標程式庫時， **SQLFetchScroll**的呼叫不能與**SQLFetch**或**SQLExtendedFetch**的呼叫混合使用。  
  
 使用資料指標程式庫時，ODBC 2 會支援**SQLFetchScroll**的呼叫。*x*和（適用于 ODBC 3）。*x*驅動程式。  
  
## <a name="rowset-buffers"></a>資料列集緩衝區  
 游標程式庫會將驅動程式資料的傳輸優化至應用程式所提供的資料列集緩衝區，前提是：  
  
-   應用程式會使用資料列取向的系結。  
  
-   應用程式所宣告來保存資料列的結構中，欄位之間沒有未使用的位元組。  
  
-   **SQLFetch**或**SQLFetchScroll**傳回資料行之長度/指標的欄位會遵循該資料行的緩衝區，然後在下一個資料行的緩衝區前面。 這些欄位為選擇性。  
  
 當應用程式要求新的資料列集時，資料指標程式庫會視需要從其快取和驅動程式中抓取資料。 如果新舊資料列集重迭，則資料指標程式庫可以重複使用資料列集緩衝區重迭區段中的資料，以優化其效能。 因此，除非新的和舊的資料列集重迭，而且變更是在資料列集緩衝區的重迭區段中，否則資料列集緩衝區的未儲存變更會遺失。 若要儲存變更，應用程式會提交定位的 update 語句。  
  
 請注意，當應用程式呼叫**SQLFetchScroll**並將*FetchOrientation*引數設為 SQL_FETCH_RELATIVE，而且*FetchOffset*引數設定為0時，資料指標程式庫一律會使用快取中的資料重新整理資料列集緩衝區。  
  
 資料指標程式庫支援以 SQL_ATTR_ROW_ARRAY_SIZE 的*屬性*呼叫**SQLSetStmtAttr** ，以在資料指標開啟時變更資料列集大小。 新的資料列集大小將在下一次呼叫**SQLFetchScroll**時生效。  
  
## <a name="result-set-membership"></a>結果集成員資格  
 游標程式庫只會在應用程式要求時，從驅動程式抓取資料。 視資料來源和 SQL_CONCURRENCY 語句屬性的設定而定，這會產生下列結果：  
  
-   資料指標程式庫所抓取的資料，可能與執行語句時可用的資料不同。 例如，在開啟資料指標之後，某些驅動程式可以抓取在目前資料指標位置以外的時間點所插入的資料列。  
  
-   資料指標程式庫的資料來源可能會鎖定結果集中的資料，因此其他使用者無法使用。  
  
 在資料指標程式庫快取一列資料之後，它就無法偵測基礎資料來源中對該資料列所做的變更（除了定點更新和刪除作業在相同游標的快取上）。 發生這種情況的原因是，對於**SQLFetchScroll**的呼叫，資料指標程式庫永遠不會從資料來源 refetches 資料。 相反地，它會從其快取中 refetches 資料。  
  
## <a name="scrolling"></a>捲動  
 資料指標程式庫支援**SQLFetchScroll**中的下列提取類型。  
  
|資料指標類型|提取類型|  
|-----------------|-----------------|  
|順向|SQL_FETCH_NEXT|  
|靜態|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 當呼叫**SQLFetchScroll** ，而且其中一個**SQLFetch**的呼叫傳回 SQL_ERROR 時，資料指標程式庫會繼續進行，如下所示。 完成這些步驟之後，資料指標程式庫會繼續處理。  
  
1.  呼叫**SQLGetDiagRec**以從驅動程式取得錯誤資訊，並將此內容張貼為驅動程式管理員中的診斷記錄。  
  
2.  將診斷記錄中的 SQL_DIAG_ROW_NUMBER 欄位設定為適當的值。  
  
3.  將診斷記錄中的 SQL_DIAG_COLUMN_NUMBER 欄位設定為適當的值（如果適用）。否則，它會將它設定為0。  
  
4.  將資料列狀態陣列中發生錯誤之資料列的值設定為 SQL_ROW_ERROR。  
  
 當資料指標程式庫在其**SQLFetchScroll**的執行中多次呼叫**SQLFetch**之後，其中一個對**SQLFetch**的呼叫所傳回的任何錯誤或警告都會在診斷記錄中，而且可透過呼叫**SQLGetDiagRec**來抓取。 如果資料在提取時遭到截斷，則已截斷的資料現在會位於游標程式庫的快取中。 後續呼叫**SQLFetchScroll**以滾動到具有截斷資料的資料列時，將會傳回截斷的資料，而且不會產生警告，因為資料是從游標程式庫的快取中提取。 為了追蹤傳回的資料長度，使其可以判斷緩衝區中傳回的資料是否已被截斷，應用程式應該系結長度/指標緩衝區。  
  
## <a name="bookmark-operations"></a>書簽作業  
 資料指標程式庫支援以 SQL_FETCH_BOOKMARK 的*FetchOrientation*呼叫**SQLFetchScroll** 。 它也支援在*FetchOffset*引數中指定可用於書簽作業的位移。 這是資料指標程式庫唯一支援的書簽作業。 資料指標程式庫不支援呼叫**SQLBulkOperations**。  
  
 如果應用程式已設定 SQL_ATTR_USE_BOOKMARKS 語句屬性，並且已系結至書簽資料行，則資料指標程式庫會產生固定長度的書簽，並將其傳回給應用程式。 資料指標程式庫會建立並維護其使用的書簽;它不會使用在資料來源維護的書簽。 當呼叫**SQLFetchScroll**來取得已從資料來源提取的資料區塊時，它會從游標程式庫快取中抓取資料。 因此，在呼叫**SQLFetchScroll**時使用*FetchOrientation* SQL_FETCH_BOOKMARK 的書簽，必須由資料指標程式庫來建立及維護。  
  
## <a name="interaction-with-other-functions"></a>與其他功能的互動  
 應用程式必須先呼叫**SQLFetch**或**SQLFetchScroll** ，才能準備或執行任何定位的 update 或 delete 語句。
