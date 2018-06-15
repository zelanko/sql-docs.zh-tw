---
title: Long 資料和 SQLSetPos SQLBulkOperations |Microsoft 文件
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
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c5734480db4ac3b8098254a4c99dbf7a361ea3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913933"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 資料和 SQLSetPos SQLBulkOperations
更新資料列時，使用 SQL 陳述式中的參數案例一樣，可以傳送長資料**SQLBulkOperations**或**SQLSetPos**或插入資料列時**SQLBulkOperations**. 資料會使用多個呼叫的組件，以傳送**SQLPutData**。 在執行階段資料會傳送的資料行稱為*資料在執行中資料行*。  
  
> [!NOTE]  
>  應用程式實際上可以傳送任何類型的資料在執行階段使用**SQLPutData**，不過，當傳送只字元和二進位資料部分。 不過，如果資料夠小，無法容納在單一緩衝區中，沒有通常沒有必要使用**SQLPutData**。 會比較容易緩衝區繫結，讓驅動程式從緩衝區中擷取資料。  
  
 長資料行通常不會繫結，因為應用程式必須將繫結的資料行，然後再呼叫**SQLBulkOperations**或**SQLSetPos**和先解除繫結之後呼叫**SQLBulkOperations**或**SQLSetPos**。 必須繫結資料行，因為**SQLBulkOperations**或**SQLSetPos**只在繫結資料行上作業，而且必須是未繫結，讓**SQLGetData**可以用來擷取資料從資料行。  
  
 若要在執行階段傳送資料，應用程式會執行下列動作：  
  
1.  將 32 位元值放在資料列集緩衝區，而不是資料值。 這個值會傳回更新版本中，應用程式，讓應用程式應該將它設定為有意義的值，例如資料行的數目或包含資料的檔案控制代碼。  
  
2.  設定 SQL_LEN_DATA_AT_EXEC 結果的長度/指標緩衝區中的值 (*長度*) 巨集。 這個值會指示驅動程式的參數的資料會傳送具有**SQLPutData**。 *長度*長資料傳送至需要知道將會傳送多少位元組長的資料，使它可以預先配置空間的資料來源時，會使用值。 若要判斷資料來源是否需要此值，應用程式會呼叫**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 選項。 所有驅動程式必須支援這個巨集;如果資料來源不需要的位元組長度，此驅動程式可以忽略它。  
  
3.  呼叫**SQLBulkOperations**或**SQLSetPos**。 驅動程式可讓您探索長度/指標緩衝區包含結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集，並傳回 SQL_NEED_DATA，做為函式的傳回值。  
  
4.  呼叫**SQLParamData** SQL_NEED_DATA 的回應中傳回的值。 如果很長的資料需要傳送， **SQLParamData**傳回 SQL_NEED_DATA。 所指向之緩衝區中*ValuePtrPtr*引數，驅動程式會傳回應用程式放在緩衝區資料列集的唯一值。 如果有一個以上的資料在執行資料行，則應用程式會使用這個值來判斷要傳送的資料進行; 資料行驅動程式不需要要求資料在執行任何特定順序的資料行的資料。  
  
5.  呼叫**SQLPutData**驅動程式傳送資料行的資料。 如果資料行的資料無法容納在單一緩衝區中，通常都是使用 long 資料的情況下，應用程式呼叫**SQLPutData**重複將資料傳送部分; 負責的驅動程式和資料來源重新組合的資料。 如果應用程式傳遞 null 結束的字串資料時，驅動程式或資料來源必須移除 null 結束的字元重組程序的一部分。  
  
6.  呼叫**SQLParamData**再次以表示它已傳送所有資料行的資料。 如果有任何資料在執行中資料行的資料尚未傳送，驅動程式會傳回 SQL_NEED_DATA 和下一步 的資料在執行資料行; 的唯一值應用程式會傳回至步驟 5。 如果資料已傳送的所有資料在執行資料行，資料列的資料會傳送至資料來源。 **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回任何 SQLSTATE，則**SQLBulkOperations**或**SQLSetPos**可以傳回。  
  
 之後**SQLBulkOperations**或**SQLSetPos**傳回 SQL_NEED_DATA 和最後一個資料執行資料行已完全傳送資料之前，陳述式是在需要的資料狀態。 在這個狀態下，應用程式只可以呼叫**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函式會傳回 SQLSTATE HY010 （函數順序錯誤）。 呼叫**SQLCancel**取消執行陳述式並傳回其先前的狀態。 如需詳細資訊，請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
