---
title: 長數據和 SQLSetPos 和 SQLBulk 操作 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bc6c5d2da2f796a7c312971635fc36bc2fae8af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287862"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>長資料和 SQLSetPos 與 SQLBulkOperations
與 SQL 語句中的參數一樣,使用**SQLBulk 操作**或**SQLSetPos**更新行或使用**SQLBulk 操作**插入行時,可以發送長數據。 數據分件發送,對**SQLPutData**進行多次調用。 在執行時傳送資料的欄位稱為*執行時的資料欄*位 。  
  
> [!NOTE]  
>  應用程序實際上可以使用**SQLPutData**在執行時發送任何類型的數據,儘管只能分批發送字元和二進位數據。 但是,如果資料足夠小,可以容納單個緩衝區,則通常沒有理由使用**SQLPutData**。 綁定緩衝區並讓驅動程式從緩衝區檢索數據要容易得多。  
  
 由於長數據列通常不綁定,因此應用程式必須在調用**SQLBulk 操作**或**SQLSetPos**之前綁定列,並在調用**SQLBulk 操作**或**SQLSetPos**後取消綁定該列。 必須綁定該列,因為**SQLBulk 操作**或**SQLSetPos**僅在綁定列上操作,並且必須取消綁定,以便**SQLGetData**可用於從列中檢索數據。  
  
 在執行時傳送資料,應用程式執行以下操作:  
  
1.  在行集緩衝區中放置 32 位值,而不是數據值。 此值稍後將返回到應用程式,因此應用程式應將其設置為有意義的值,例如列數或包含數據的檔的句柄。  
  
2.  將長度/指示器緩衝區中的值設置為 SQL_LEN_DATA_AT_EXEC(*長度*) 宏的結果。 此值向驅動程式指示參數的數據將與**SQLPutData**一起發送。 將長數據發送到數據源時,將使用*長度*值,數據源需要知道將發送多少位元組的長數據,以便它可以預分配空間。 要確定資料來源是否需要此值,應用程式使用SQL_NEED_LONG_DATA_LEN選項調用**SQLGetInfo。** 所有驅動程式都必須支援此宏;所有驅動程式都必須支援此宏。如果數據源不需要位元組長度,驅動程式可以忽略它。  
  
3.  呼叫**SQLBulk 操作或** **SQLSetPos**。 驅動程式發現長度/指示器緩衝區包含SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果,並將返回SQL_NEED_DATA作為函數的返回值。  
  
4.  調用**SQLParamData**以回應SQL_NEED_DATA返回值。 如果需要發送長數據 **,SQLParamData**將返回SQL_NEED_DATA。 在*ValuePtrPtr*參數指向的緩衝區中,驅動程式返回應用程式放置在行集緩衝區中的唯一值。 如果存在多個執行數據列,則應用程式使用此值來確定要為其發送數據的列;驅動程式不需要按任何特定順序請求數據執行列的數據。  
  
5.  呼叫**SQLPutData**將列資料傳送到驅動程式。 如果列數據不適合單個緩衝區(與長數據通常的情況一樣),應用程式將重複調用 SQLPutData 以分部發送數據;如果列數據與長數據一樣,則調用 SQLPutData 以發送部分數據;如果列數據不適合使用,則調用**SQLPutData**以部分發送數據。由驅動程式和數據源重新組合數據。 如果應用程式傳遞 null 終止字串資料,驅動程式或數據源必須刪除 null 終止字元作為重新組裝過程的一部分。  
  
6.  再次調用**SQLParamData**以指示它已發送了該列的所有數據。 如果有任何未為其發送數據的數據執行列,則驅動程式將返回SQL_NEED_DATA和下一個執行數據列的唯一值;應用程式返回到步驟 5。 如果已為執行時的所有數據列發送數據,則該行的數據將發送到數據源。 **然後,SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,並可以返回**SQLBulk 操作**或**SQLSetPos**可以返回的任何 SQLSTATE。  
  
 **在 SQLBulk 操作**或**SQLSetPos**傳回SQL_NEED_DATA後,在已為執行時的最後一個資料列完全發送數據之前,該語句處於"需要資料" 在此狀態下,應用程式只能調用 SQLPutData、SQLParamData、SQLCancel、SQLGetDiagField 或**SQLGetDiagRec;** **SQLPutData** **SQLParamData** **SQLCancel** **SQLGetDiagField**所有其他函數返回 SQLSTATE HY010(函數序列錯誤)。 調用**SQLCancel**會取消語句的執行並將其返回到其以前的狀態。 關於詳細資訊,請參閱附錄[B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
