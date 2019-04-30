---
title: Long 資料和 SQLSetPos 與 SQLBulkOperations |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d1a55d3b417ff7a0a673bda8d289a72d7c1cb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312857"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>長資料和 SQLSetPos 與 SQLBulkOperations
更新資料列時，在此情況下，使用 SQL 陳述式中的參數，可以傳送長資料**SQLBulkOperations**或是**SQLSetPos**或插入資料列時**SQLBulkOperations**. 資料會使用多個呼叫的組件，以傳送**SQLPutData**。 為其資料會在執行階段傳送的資料行稱為*資料在執行中資料行*。  
  
> [!NOTE]  
>  應用程式實際上可以傳送任何類型的資料在執行階段使用**SQLPutData**，不過，在組件，則會傳送只字元和二進位資料。 不過，如果資料夠小，無法放入單一緩衝區中，有通常是使用沒有理由**SQLPutData**。 很容易繫結緩衝區，並讓驅動程式從緩衝區中擷取資料。  
  
 長資料行通常不會繫結，因為應用程式必須繫結的資料行，然後再呼叫**SQLBulkOperations**或是**SQLSetPos**和 unbind 之後呼叫**SQLBulkOperations**或是**SQLSetPos**。 必須繫結資料行，因為**SQLBulkOperations**或是**SQLSetPos**只在繫結資料行，而且必須是未繫結，讓**SQLGetData**可以用來擷取資料從資料行。  
  
 若要在執行階段傳送資料，應用程式會執行下列作業：  
  
1.  32 位元會將值放在資料列集緩衝區，而不是資料值。 會在應用程式之後，傳回此值，因此應用程式應該將它設定為有意義的值，例如資料行的數字或包含資料的檔案控制代碼。  
  
2.  設定 SQL_LEN_DATA_AT_EXEC 結果的長度/指標緩衝區中的值 (*長度*) 巨集。 這個值會指示驅動程式的參數的資料將會傳送具有**SQLPutData**。 *長度*將長資料傳送至資料來源，必須知道會傳送多少個位元組的 long 資料，以便讓它可以預先配置空間時，會使用值。 若要判斷資料來源是否需要此值，應用程式會呼叫**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 選項。 所有驅動程式必須支援這個巨集;如果資料來源不需要的位元組長度，此驅動程式可以忽略它。  
  
3.  呼叫**SQLBulkOperations**或是**SQLSetPos**。 驅動程式可讓您探索長度/指標緩衝區包含結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集，並傳回 SQL_NEED_DATA 函式的傳回值。  
  
4.  呼叫**SQLParamData** SQL_NEED_DATA 的回應中傳回的值。 如果需要傳送長資料**SQLParamData**會傳回 SQL_NEED_DATA。 中所指向的緩衝區*ValuePtrPtr*引數，驅動程式會傳回應用程式放在緩衝區資料列集的唯一值。 如果有一個以上的資料在執行資料行，則應用程式會使用此值來判斷要傳送資料; 資料行驅動程式不需要要求資料在執行任何特定順序的資料行的資料。  
  
5.  呼叫**SQLPutData**驅動程式傳送的資料行資料。 如果資料行的資料無法容納在單一緩衝區中，通常就是 long 資料的情況，應用程式會呼叫**SQLPutData**不斷地傳送部分; 中的資料是由驅動程式和資料來源來重組資料。 如果應用程式傳遞 null 結束的字串資料，驅動程式或資料來源必須移除 null 終止的字元重組程序的一部分。  
  
6.  呼叫**SQLParamData**以表示它已傳送所有資料行的資料。 如果有為其資料尚未傳送任何資料執行資料行，驅動程式會傳回 SQL_NEED_DATA 和下一步 的資料在執行資料行; 的唯一值應用程式會返回步驟 5。 如果資料已傳送的所有資料在執行資料行，資料列的資料會傳送至資料來源。 **SQLParamData**則會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回任何 SQLSTATE 所**SQLBulkOperations**或是**SQLSetPos**可以傳回。  
  
 在後**SQLBulkOperations**或是**SQLSetPos**會傳回 SQL_NEED_DATA 且資料已完全傳送最後一個資料在執行中資料行之前，陳述式中需要的資料狀態。 在此狀態下，應用程式可以只呼叫**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函式會傳回 SQLSTATE HY010 （函數順序錯誤）。 呼叫**SQLCancel**取消執行陳述式，並傳回其先前的狀態。 如需詳細資訊，請參閱[附錄 b:狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
