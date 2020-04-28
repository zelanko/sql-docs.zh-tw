---
title: 傳送長資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304179"
---
# <a name="sending-long-data"></a>傳送長資料
Dbms 會將*長資料*定義為任何一種大小的字元或二進位資料，例如254個字元。 可能無法在記憶體中儲存長資料的整個專案，例如當專案代表長文字檔或點陣圖時。 因為這類資料無法儲存在單一緩衝區中，所以當執行語句時，資料來源會將它傳送給具有**SQLPutData**的元件中的驅動程式。 在執行時間傳送資料的參數稱為*資料執行中參數*。  
  
> [!NOTE]  
>  應用程式可以在執行時間使用**SQLPutData**來傳送任何類型的資料，雖然只有字元和二進位資料可以在部分中傳送。 不過，如果資料夠小而足以容納在單一緩衝區中，通常就沒有使用**SQLPutData**的理由。 系結緩衝區更為容易，並讓驅動程式從緩衝區抓取資料。  
  
 若要在執行時間傳送資料，應用程式會執行下列動作：  
  
1.  傳遞32位值，以識別**SQLBindParameter**中*ParameterValuePtr*引數的參數，而不是傳遞緩衝區的位址。 驅動程式不會分析此值。 稍後會將它傳回給應用程式，因此它應該代表應用程式的內容。 例如，它可能是參數的數目或包含資料之檔案的控制碼。  
  
2.  在**SQLBindParameter**的*StrLen_or_IndPtr*引數中傳遞長度/指標緩衝區的位址。  
  
3.  將 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果儲存在長度/指標緩衝區中。 這兩個值都會向驅動程式指出參數的資料會與**SQLPutData**一起傳送。 將長資料傳送至資料來源時，會使用 SQL_LEN_DATA_AT_EXEC （*長度*），這需要知道將傳送多少位元組的長資料，使其可以預先配置空間。 為了判斷資料來源是否需要此值，應用程式會使用 SQL_NEED_LONG_DATA_LEN 選項來呼叫**SQLGetInfo** 。 所有的驅動程式都必須支援此宏;如果資料來源不需要位元組長度，則驅動程式可以忽略它。  
  
4.  呼叫**SQLExecute**或**SQLExecDirect**。 驅動程式會探索長度/指標緩衝區包含值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果，並傳回 SQL_NEED_DATA 做為函數的傳回值。  
  
5.  呼叫**SQLParamData**以回應 SQL_NEED_DATA 傳回值。 如果需要傳送較長的資料， **SQLParamData**會傳回 SQL_NEED_DATA。 在*ValuePtrPtr*引數所指向的緩衝區中，驅動程式會傳回識別資料執行中參數的值。 如果有一個以上的資料執行中參數，應用程式必須使用此值來判斷要傳送資料的參數。不需要此驅動程式，就能以任何特定順序要求資料執行中參數的資料。  
  
6.  呼叫**SQLPutData**以傳送參數資料給驅動程式。 如果參數資料無法放入單一緩衝區中，通常是長資料的情況，應用程式會重複呼叫**SQLPutData**來傳送部分資料;驅動程式和資料來源會負責重組資料。 如果應用程式傳遞以 null 結束的字串資料，則驅動程式或資料來源必須在重新組合過程中移除 null 終止字元。  
  
7.  再次呼叫**SQLParamData** ，表示它已傳送參數的所有資料。 如果有任何資料執行中參數尚未傳送資料，驅動程式會傳回 SQL_NEED_DATA 和識別下一個參數的值;應用程式會回到步驟6。 如果已傳送所有資料執行中參數的資料，則會執行語句。 **SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回**SQLExecute**或**SQLExecDirect**可以傳回的任何傳回值或診斷。  
  
 在**SQLExecute**或**SQLExecDirect**傳回 SQL_NEED_DATA，而且在資料已完全傳送至最後一個資料執行中參數之前，語句就會是需要資料狀態。 當語句處於需要資料狀態時，應用程式只能呼叫**SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**或**SQLGetDiagRec**;所有其他函式會傳回 SQLSTATE HY010 （函數序列錯誤）。 呼叫**SQLCancel**會取消語句的執行，並將它傳回至先前的狀態。 如需詳細資訊，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需在執行時間傳送資料的範例，請參閱[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函數描述。
