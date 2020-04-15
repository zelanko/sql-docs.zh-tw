---
title: SQLFetchScroll(游標庫) |微軟文件
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
ms.openlocfilehash: e5573b8afc49afec8b7afa4fc52590e7a6a9e2fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302049"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLFetchScroll**函數。 有關**SQLFetchScroll 的**一般資訊,請參閱[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 游標庫透過在驅動程式中重複調用**SQLFetch**實現**SQLFetch。** 它將從驅動程式檢索到的數據傳輸到應用程式提供的行集緩衝區。 它還將數據緩存在記憶體和磁碟檔中。 當應用程式請求新的行集時,遊標庫根據需要從驅動程式(如果以前未提取)或緩存(如果以前已提取)中檢索它。 最後,游標庫維護緩存數據的狀態,並將此資訊返回到行狀態陣列中的應用程式。  
  
 使用游標庫時,對**SQLFetchScroll**的調用不能與**SQLFetch**或**SQL 擴展獲取的**調用混合。  
  
 使用游標庫時,ODBC 2 都支援對**SQLFetchScroll 的**調用。*x*和 ODBC 3。*x*驅動程式。  
  
## <a name="rowset-buffers"></a>行集緩衝區  
 在以下情況下,游標庫優化了數據從驅動程式傳輸到應用程式提供的行集緩衝區:  
  
-   應用程式使用行綁定。  
  
-   應用程式聲明為保存一行數據的結構中的欄位之間沒有未使用的位元組。  
  
-   **SQLFetch**或**SQLFetchScroll**傳回列的長度/指示器的欄位遵循該列的緩衝區,並在下一列的緩衝區之前。 這些欄位為選擇性。  
  
 當應用程式請求新的行集時,游標庫根據需要從其緩存和驅動程序檢索數據。 如果新舊行集重疊,游標庫可以通過重用行集緩衝區重疊部分的數據來優化其性能。 因此,除非新舊行集重疊,並且更改位於行集緩衝區的重疊部分,否則將丟失對行集緩衝區的未保存更改。 要保存更改,應用程式將提交定位的更新語句。  
  
 請注意,當應用程式調用**SQLFetchScroll**時,游標庫始終使用緩存中的數據刷新行集緩衝區,其中*Fetch 定向*參數設置為SQL_FETCH_RELATIVE,FetchOffset*FetchOffset*參數設置為 0。  
  
 游標庫支援使用SQL_ATTR_ROW_ARRAY_SIZE*屬性*調用**SQLSetStmtAttr,** 以在游標打開時更改行集大小。 下次調用**SQLFetchScroll**時,新的行集大小將生效。  
  
## <a name="result-set-membership"></a>結果集成員資格  
 游標庫僅在應用程式請求時從驅動程式檢索數據。 根據資料來源和SQL_CONCURRENCY語句屬性的設置,這會產生以下後果:  
  
-   游標庫檢索的數據可能與執行語句時可用的數據不同。 例如,在打開游標後,某些驅動程式可以檢索插入在當前游標位置以外的點插入的行。  
  
-   結果集中的數據可能由游標庫的數據源鎖定,因此其他使用者不可用。  
  
 游標庫快取一行資料後,無法偵測對基礎資料來源中該行的更改(定位更新和在同一游標緩存上運行的刪除除外)。 這是因為,對於**SQLFetchScroll 的**調用,遊標庫從不從數據源重新提取數據。 相反,它會從緩存中重新提取數據。  
  
## <a name="scrolling"></a>捲動  
 游標庫支援**SQLFetchScroll**中的以下提取類型。  
  
|資料指標類型|擷取類型|  
|-----------------|-----------------|  
|順向|SQL_FETCH_NEXT|  
|靜態|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 當調用**SQLFetchScroll**並返回**SQLFetch**的調用之一SQL_ERROR時,游標庫將如下所示。 完成這些步驟后,游標庫將繼續處理。  
  
1.  調用**SQLGetDiagRec**從驅動程式獲取錯誤資訊,並將其作為診斷記錄張貼在驅動程式管理器中。  
  
2.  將診斷記錄中SQL_DIAG_ROW_NUMBER欄位設置為適當的值。  
  
3.  將診斷記錄中的SQL_DIAG_COLUMN_NUMBER欄位設置為適當的值(如果適用);否則,它將設置為 0。  
  
4.  將行狀態陣列中出錯行的值設置為SQL_ROW_ERROR。  
  
 游標庫在實現**SQLFetchScroll**時多次調用**SQLFetch**後,對**SQLFetch**的調用返回的任何錯誤或警告都將位於診斷記錄中,並且可以通過調用**SQLGetDiagRec**來檢索。 如果數據在提取時被截斷,則截斷的數據現在將駐留在游標庫的緩存中。 後續對**SQLFetchScroll**的呼叫以滾動到具有截斷數據的行將返回截斷的數據,並且不會引發任何警告,因為數據是從游標庫的緩存中獲取的。 為了跟蹤返回的數據長度,以便確定緩衝區中返回的數據是否已截斷,應用程式應綁定長度/指示器緩衝區。  
  
## <a name="bookmark-operations"></a>書籤操作  
 游標庫支援使用SQL_FETCH_BOOKMARK*的取取方向*呼叫**SQLFetchScroll。** 它還支援在 *「提取偏移」* 參數中指定可在書籤操作中使用的偏移量。 這是游標庫支援的唯一書簽操作。 游標庫不支援呼叫**SQLBulk 操作**。  
  
 如果應用程式已設置SQL_ATTR_USE_BOOKMARKS語句屬性並綁定到書籤列,則游標庫將生成一個固定長度的書籤並將其返回到應用程式。 游標庫創建和維護它使用的書籤;它不使用在數據源中維護的書籤。 當調用**SQLFetchScroll**來檢索已經從數據來源取得的數據塊時,它會從游標庫緩存中檢索數據。 因此,在調用**SQLFetchScroll**時使用的書籤(帶有SQL_FETCH_BOOKMARK*的取取方向*必須由游標庫創建和維護。  
  
## <a name="interaction-with-other-functions"></a>與其他函數的互動  
 應用程式必須調用**SQLFetch**或**SQLFetchScroll,** 然後才能準備或執行任何定位的更新或刪除語句。
