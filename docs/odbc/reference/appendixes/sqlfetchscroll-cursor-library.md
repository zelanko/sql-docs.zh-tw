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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086447"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLFetchScroll**資料指標程式庫中的函式。 如需一般資訊**SQLFetchScroll**，請參閱[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 資料指標程式庫會實作**SQLFetchScroll**藉由重複呼叫**SQLFetch**驅動程式中。 它將會擷取來自驅動程式應用程式所提供的資料列集緩衝區資料的傳輸。 它也會在記憶體和磁碟的檔案中的資料快取。 當應用程式要求新的資料列集時，資料指標程式庫擷取其視需要從驅動程式 （如果它尚未先前提取） 或快取 （如果先前擷取）。 最後，資料指標程式庫會維護快取資料的狀態，並傳回資料列狀態陣列中的應用程式的這項資訊。  
  
 使用資料指標程式庫時，呼叫**SQLFetchScroll**不得與呼叫**SQLFetch**或是**SQLExtendedFetch**。  
  
 使用資料指標程式庫時，呼叫**SQLFetchScroll**所支援的 ODBC 2。*x*和適用於 ODBC 3。*x*驅動程式。  
  
## <a name="rowset-buffers"></a>資料列集的緩衝區  
 資料指標程式庫可最佳化資料可從 驅動程式傳送至應用程式提供，如果資料列集的緩衝區：  
  
-   應用程式會使用資料列取向的繫結。  
  
-   結構宣告來保存資料列的應用程式中的欄位之間有任何未使用的位元組。  
  
-   中的欄位**SQLFetch**或是**SQLFetchScroll**傳回長度/指標資料行之後，該資料行的緩衝區，而且前面出現下一個資料行的緩衝區。 這些欄位為選擇性。  
  
 當應用程式要求新的資料列集時，資料指標程式庫從其快取，並視需要的驅動程式，就會擷取資料。 如果新的和舊的資料列集重疊，資料指標程式庫可以重複使用的資料列集緩衝區重疊的各節中的資料最佳化其效能。 因此，對資料列集緩衝區所作的變更都會遺失，除非新的和舊的資料列集重疊而變更的資料列集緩衝區重疊的各節中。 若要儲存所做的變更，應用程式會提交定位的 update 陳述式。  
  
 請注意，資料指標程式庫一律會重新整理資料列集緩衝區快取的資料時應用程式呼叫**SQLFetchScroll**具有*Sqlfetchscroll*引數設定為 sql_fetch_relative 但和*FetchOffset*引數設定為 0。  
  
 資料指標程式庫支援呼叫**SQLSetStmtAttr**具有*屬性*的 SQL_ATTR_ROW_ARRAY_SIZE 來開啟資料指標時，變更資料列集大小。 新的資料列集大小才會生效，下次**SQLFetchScroll**呼叫。  
  
## <a name="result-set-membership"></a>結果集的成員資格  
 資料指標程式庫的驅動程式擷取資料，只有在應用程式要求它。 根據資料來源和 SQL_CONCURRENCY 陳述式屬性的設定，這會有下列結果：  
  
-   擷取資料指標程式庫的資料可能會有所不同時可用的時間執行的陳述式的資料。 比方說，資料指標開啟後，目前的游標位置之後的某一點中插入資料列可以擷取部分驅動程式。  
  
-   在結果集中的資料可能由資料指標程式庫的資料來源鎖定，並因此無法對其他使用者。  
  
 資料指標程式庫已快取的資料列之後，就無法在基礎資料來源 （除了定位的更新及刪除操作相同的資料指標快取） 中偵測到該資料列的變更。 這是因為，呼叫**SQLFetchScroll**，資料指標程式庫永遠不會 refetches 從資料來源的資料。 相反地，它 refetches 從其快取的資料。  
  
## <a name="scrolling"></a>捲動  
 資料指標程式庫支援中的下列提取類型**SQLFetchScroll**。  
  
|資料指標類型|擷取型別|  
|-----------------|-----------------|  
|順向|SQL_FETCH_NEXT|  
|Static|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>錯誤  
 當**SQLFetchScroll**呼叫，呼叫的另一個**SQLFetch**傳回 SQL_ERROR，資料指標程式庫會繼續進行，如下所示。 完成這些步驟之後，資料指標程式庫會繼續處理。  
  
1.  呼叫**SQLGetDiagRec**以取得錯誤資訊的驅動程式，並將此張貼為驅動程式管理員中的診斷記錄。  
  
2.  SQL_DIAG_ROW_NUMBER 將欄位設定為適當值的診斷記錄中。  
  
3.  在 診斷記錄，以適當的值，設定 SQL_DIAG_COLUMN_NUMBER 欄位，如果適用;否則，它將它設定為 0。  
  
4.  SQL_ROW_ERROR 資料列狀態陣列中的錯誤設定的資料列的值。  
  
 資料指標之後已呼叫的程式庫**SQLFetch**多次在實作**SQLFetchScroll**，任何錯誤或其中一個呼叫所傳回的警告**SQLFetch**會在診斷記錄，可以擷取由呼叫**SQLGetDiagRec**。 如果資料已截斷時擷取，截斷的資料都將會現在位於 資料指標程式庫的快取。 後續呼叫**SQLFetchScroll**捲動的資料列來截斷的資料將會傳回截斷的資料，並會引發任何警告，因為會從資料指標程式庫的快取中擷取的資料。 若要追蹤的資料傳回，以便它可以判斷是否傳回緩衝區中的資料已截斷的長度，應用程式應繫結之長度/指標緩衝區。  
  
## <a name="bookmark-operations"></a>書籤的作業  
 資料指標程式庫支援呼叫**SQLFetchScroll**具有*Sqlfetchscroll*要使用 sql_fetch_bookmark。 它也支援指定的位移*FetchOffset*可用在書籤作業的引數。 這是唯一的書籤作業的資料指標程式庫支援。 資料指標程式庫不支援呼叫**SQLBulkOperations**。  
  
 如果應用程式已設定 SQL_ATTR_USE_BOOKMARKS 陳述式屬性，且已繫結至書籤資料行，資料指標程式庫會產生固定長度書籤，並傳回應用程式。 資料指標程式庫會建立和維護它會使用; 書籤它不會使用書籤保留在資料來源。 當**SQLFetchScroll**呼叫以擷取從資料來源已經提取的資料區塊，它會擷取資料從資料指標程式庫快取。 如此一來，書籤用於呼叫**SQLFetchScroll**具有*Sqlfetchscroll*的 SQL_FETCH_BOOKMARK 必須是所建立和維護資料指標程式庫。  
  
## <a name="interaction-with-other-functions"></a>與其他函式之間的互動  
 應用程式必須呼叫**SQLFetch**或是**SQLFetchScroll**它準備或執行之前任何定位的 update 或 delete 陳述式。
