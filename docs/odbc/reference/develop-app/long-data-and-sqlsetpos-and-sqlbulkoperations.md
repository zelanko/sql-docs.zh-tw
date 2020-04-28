---
title: 長資料和 SQLSetPos 和 SQLBulkOperations |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287862"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>長資料和 SQLSetPos 與 SQLBulkOperations
就像 SQL 語句中的參數一樣，使用**SQLBulkOperations**或**SQLSetPos**來更新資料列時，或使用**SQLBulkOperations**插入資料列時，可以傳送較長的資料。 資料會在元件中傳送，且會多次呼叫**SQLPutData**。 在執行時間傳送資料的資料行稱為「*資料執行中」資料行*。  
  
> [!NOTE]  
>  應用程式實際上可以在執行時間使用**SQLPutData**傳送任何類型的資料，雖然只有字元和二進位資料可以在部分中傳送。 不過，如果資料夠小而足以容納在單一緩衝區中，通常就沒有使用**SQLPutData**的理由。 系結緩衝區更為容易，並讓驅動程式從緩衝區抓取資料。  
  
 因為較長的資料行通常不會系結，所以應用程式在呼叫**SQLBulkOperations**或**SQLSetPos**之前必須先系結資料行，並在呼叫**SQLBulkOperations**或**SQLSetPos**之後將它解除系結。 必須系結資料行，因為**SQLBulkOperations**或**SQLSetPos**只會在系結資料行上運作，而且必須解除系結，才能使用**SQLGetData**來抓取資料行中的資料。  
  
 若要在執行時間傳送資料，應用程式會執行下列動作：  
  
1.  將32位值放在資料列集緩衝區中，而不是資料值。 此值稍後會傳回給應用程式，因此應用程式應該將它設定為有意義的值，例如資料行的數目或包含資料的檔案控制碼。  
  
2.  將長度/指標緩衝區中的值設定為 SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果。 這個值會向驅動程式指出參數的資料會與**SQLPutData**一起傳送。 將長資料傳送至資料來源時，會使用*長度*值，這需要知道將會傳送多少位元組的長資料，使其可以預先配置空間。 為了判斷資料來源是否需要此值，應用程式會使用 SQL_NEED_LONG_DATA_LEN 選項來呼叫**SQLGetInfo** 。 所有的驅動程式都必須支援此宏;如果資料來源不需要位元組長度，則驅動程式可以忽略它。  
  
3.  呼叫**SQLBulkOperations**或**SQLSetPos**。 驅動程式會探索長度/指標緩衝區包含 SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果，並傳回 SQL_NEED_DATA 做為函數的傳回值。  
  
4.  呼叫**SQLParamData**以回應 SQL_NEED_DATA 傳回值。 如果需要傳送較長的資料， **SQLParamData**會傳回 SQL_NEED_DATA。 在*ValuePtrPtr*引數所指向的緩衝區中，驅動程式會傳回應用程式放在資料列集緩衝區中的唯一值。 如果有多個執行中的資料行，應用程式會使用此值來判斷要傳送資料的資料行。不需要此驅動程式，就能以任何特定順序要求資料執行中的資料行。  
  
5.  呼叫**SQLPutData**將資料行資料傳送至驅動程式。 如果資料行資料不適合單一緩衝區，通常是長資料的情況，應用程式會重複呼叫**SQLPutData** ，以傳送部分資料。驅動程式和資料來源會負責重組資料。 如果應用程式傳遞以 null 結束的字串資料，則驅動程式或資料來源必須在重新組合過程中移除 null 終止字元。  
  
6.  再次呼叫**SQLParamData** ，表示它已傳送資料行的所有資料。 如果有任何資料執行中的資料行尚未傳送資料，驅動程式會傳回 SQL_NEED_DATA，並傳回下一個資料執行中資料行的唯一值;應用程式會返回步驟5。 如果已傳送所有資料執行中資料行的資料，則會將資料列的資料傳送至資料來源。 然後， **SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回**SQLBulkOperations**或**SQLSETPOS**可以傳回的任何 SQLSTATE。  
  
 在**SQLBulkOperations**或**SQLSetPos**傳回 SQL_NEED_DATA，而且在資料已完全傳送至最後一個資料執行中的資料行之前，語句就是需要資料狀態。 在此狀態下，應用程式只能呼叫**SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**或**SQLGetDiagRec**;所有其他函式會傳回 SQLSTATE HY010 （函數序列錯誤）。 呼叫**SQLCancel**會取消語句的執行，並將它傳回至先前的狀態。 如需詳細資訊，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
