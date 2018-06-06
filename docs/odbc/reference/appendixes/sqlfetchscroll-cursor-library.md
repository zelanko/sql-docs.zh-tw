---
title: SQLFetchScroll （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0c3e9709cd3aeced11116ab88c5323d4462abd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLFetchScroll**資料指標程式庫中的函式。 如需一般資訊**SQLFetchScroll**，請參閱[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 資料指標程式庫實作**SQLFetchScroll**重複呼叫**SQLFetch**驅動程式中。 它會傳送來自驅動程式會擷取到應用程式所提供的資料列集緩衝區的資料。 它也會在記憶體和磁碟的檔案中的資料快取。 當應用程式要求新的資料列集時，資料指標程式庫會擷取它在必要時從驅動程式 （如果它尚未先前提取） 或快取 （如果先前擷取）。 最後，資料指標程式庫會維護快取資料的狀態，並傳回資料列狀態陣列中應用程式的這項資訊。  
  
 使用資料指標程式庫時，呼叫**SQLFetchScroll**不得與呼叫**SQLFetch**或**SQLExtendedFetch**。  
  
 使用資料指標程式庫時，呼叫**SQLFetchScroll**所支援的 ODBC 2。*x*和 odbc 3。*x*驅動程式。  
  
## <a name="rowset-buffers"></a>資料列集的緩衝區  
 資料指標程式庫會最佳化資料可從驅動程式傳輸至資料列集的緩衝區時由應用程式提供：  
  
-   應用程式會使用資料列取向的繫結。  
  
-   應用程式會宣告來保存資料列的結構中，欄位之間有任何未使用的位元組。  
  
-   中的欄位**SQLFetch**或**SQLFetchScroll**傳回長度/指標資料行之後，該資料行的緩衝區，而且前面出現下一個資料行的緩衝區。 這些欄位為選擇性。  
  
 當應用程式要求新的資料列集時，資料指標程式庫會從其快取，並視需要的驅動程式擷取資料。 如果新的和舊的資料列集重疊，資料指標程式庫可以重複使用的資料列集緩衝區重疊的各節中的資料最佳化其效能。 因此，資料列集緩衝區未儲存的變更都會遺失，除非新的和舊的資料列集重疊而變更的資料列集緩衝區重疊的各節中。 若要儲存所做的變更，應用程式會提交一個定位的 update 陳述式。  
  
 請注意，資料指標程式庫一律會重新整理從快取資料的資料列集緩衝區時應用程式呼叫**SQLFetchScroll**與*Sqlfetchscroll*引數設定為 sql_fetch_relative 但和*FetchOffset*引數設定為 0。  
  
 資料指標程式庫支援呼叫**SQLSetStmtAttr**與*屬性*的 SQL_ATTR_ROW_ARRAY_SIZE 來開啟資料指標時，變更資料列集大小。 新的資料列集大小將會在下一次生效**SQLFetchScroll**呼叫。  
  
## <a name="result-set-membership"></a>結果集的成員資格  
 只有在應用程式要求資料指標程式庫的驅動程式擷取資料。 根據資料來源和 SQL_CONCURRENCY 陳述式屬性的設定，這會有下列結果：  
  
-   資料指標程式庫擷取的資料可能會因執行陳述式時所使用的資料。 例如，在開啟資料指標之後，某一點目前游標位置插入的資料列可以擷取部分驅動程式。  
  
-   在結果集中的資料可能由資料指標程式庫的資料來源鎖定，且因此無法與其他使用者。  
  
 資料指標程式庫已快取的資料列之後，就無法偵測到該資料列變更基礎資料來源 （除了定位的更新及刪除作業相同的資料指標快取） 中。 這是因為，呼叫**SQLFetchScroll**，資料指標程式庫從未 refetches 從資料來源的資料。 相反地，它 refetches 從其快取的資料。  
  
## <a name="scrolling"></a>捲動  
 資料指標程式庫支援中的下列提取類型**SQLFetchScroll**。  
  
|資料指標類型|擷取型別|  
|-----------------|-----------------|  
|順向|SQL_FETCH_NEXT|  
|靜態|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE 但<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> 要使用 SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>錯誤  
 當**SQLFetchScroll**稱為以及其中一個呼叫**SQLFetch**傳回 SQL_ERROR，資料指標程式庫會繼續進行，如下所示。 完成這些步驟之後，資料指標程式庫會繼續處理。  
  
1.  呼叫**SQLGetDiagRec**以取得錯誤資訊的驅動程式並將這張貼為驅動程式管理員中的診斷記錄。  
  
2.  SQL_DIAG_ROW_NUMBER 將欄位設定為適當值的診斷記錄中。  
  
3.  SQL_DIAG_COLUMN_NUMBER 欄位設定為適當的值，診斷記錄中，適用; 如果否則，它將它設定為 0。  
  
4.  設定資料列的值 SQL_ROW_ERROR 資料列狀態陣列中的錯誤。  
  
 在資料指標程式庫具有名為  **SQLFetch**中實作的多次**SQLFetchScroll**，任何錯誤或警告的其中一個呼叫傳回**SQLFetch**將診斷記錄，而且可以擷取由呼叫**SQLGetDiagRec**。 如果它已擷取時，資料被截斷，截斷的資料都現在位於資料指標程式庫的快取中。 後續呼叫**SQLFetchScroll**捲動至包含的資料列截斷的資料將會傳回截斷的資料，而且會引發任何警告，因為資料從資料指標程式庫的快取中提取。 若要追蹤的傳回，以便決定是否傳回緩衝區中的資料已截斷的資料長度，應用程式應繫結之長度/指標緩衝區。  
  
## <a name="bookmark-operations"></a>書籤作業  
 資料指標程式庫支援呼叫**SQLFetchScroll**與*Sqlfetchscroll*要使用 sql_fetch_bookmark。 它也支援指定的位移*FetchOffset*可以使用書籤作業中的引數。 這是唯一的書籤作業資料指標程式庫支援。 資料指標程式庫不支援呼叫**SQLBulkOperations**。  
  
 如果應用程式已設定 SQL_ATTR_USE_BOOKMARKS 陳述式屬性，而且有繫結到書籤資料行，資料指標程式庫產生固定長度的書籤，並傳回至應用程式。 資料指標程式庫建立及維護的書籤，它會使用;它不會使用書籤保留在資料來源。 當**SQLFetchScroll**稱為 「 若要擷取的已從資料來源擷取的資料區塊，它會擷取資料從資料指標程式庫快取。 如此一來，書籤用於呼叫**SQLFetchScroll**與*Sqlfetchscroll*的 SQL_FETCH_BOOKMARK 必須建立並維護的資料指標程式庫。  
  
## <a name="interaction-with-other-functions"></a>與其他函式之間的互動  
 應用程式必須呼叫**SQLFetch**或**SQLFetchScroll**它準備或執行之前放置任何 update 或 delete 陳述式。
