---
title: "傳送長資料 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f2fad149692bf76c118837daf05e0b77ebf4c38
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sending-long-data"></a>傳送長資料
Dbms 定義*long 資料*為任何字元或二進位資料超過特定大小，例如 254 個字元。 它不可能儲存在記憶體中，例如當項目所表示的長文字文件或點陣圖的長資料的整個項目。 因為這類資料無法儲存在單一緩衝區中，資料來源傳送到使用組件中的驅動程式**SQLPutData**陳述式執行時。 這在執行階段傳送的資料參數稱為*資料在執行中參數*。  
  
> [!NOTE]  
>  應用程式可以在執行階段實際傳送任何資料類型的**SQLPutData**，不過，當傳送只字元和二進位資料部分。 不過，如果資料夠小，無法容納在單一緩衝區中，沒有通常沒有必要使用**SQLPutData**。 會比較容易緩衝區繫結，讓驅動程式從緩衝區中擷取資料。  
  
 若要在執行階段傳送資料，應用程式會執行下列動作：  
  
1.  將 32 位元值，識別中的參數傳遞*ParameterValuePtr*引數中的**SQLBindParameter**而不是傳遞緩衝區的位址。 這個值就不會分析驅動程式。 它會傳回至更新版本中，應用程式，因此它應該對而言有意義的應用程式。 比方說，它可能是參數的數目或包含資料的檔案控制代碼。  
  
2.  傳遞的長度/指標緩衝區的位址*StrLen_or_IndPtr*引數的**SQLBindParameter**。  
  
3.  儲存 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 結果 (*長度*) 長度/指標緩衝區中的巨集。 兩個這些值表示驅動程式的參數的資料會傳送具有**SQLPutData**。 SQL_LEN_DATA_AT_EXEC (*長度*) 時，傳送長資料必須知道將會傳送多少位元組長的資料，使它可以預先配置空間資料來源使用。 若要判斷資料來源需要這個值，是否應用程式呼叫**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 選項。 所有驅動程式必須支援這個巨集;如果資料來源不需要的位元組長度，此驅動程式可以忽略它。  
  
4.  呼叫**SQLExecute**或**SQLExecDirect**。 驅動程式可讓您探索長度/指標緩衝區包含 SQL_DATA_AT_EXEC 的值或結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集，並傳回 SQL_NEED_DATA，做為函式的傳回值。  
  
5.  呼叫**SQLParamData** SQL_NEED_DATA 的回應中傳回的值。 如果很長的資料需要傳送， **SQLParamData**傳回 SQL_NEED_DATA。 所指向之緩衝區中*ValuePtrPtr*引數，驅動程式會傳回識別資料在執行中參數的值。 如果有一個以上的資料在執行中參數，應用程式必須使用此值來判斷哪一個參數來傳送資料。驅動程式不需要要求資料在執行任何特定順序的參數的資料。  
  
6.  呼叫**SQLPutData**將參數資料傳送到驅動程式。 如果參數資料不符合單一緩衝區中，通常都是使用 long 資料的情況下，應用程式會呼叫**SQLPutData**重複將資料傳送部分; 負責的驅動程式和資料來源重新組合的資料。 如果應用程式傳遞 null 結束的字串資料時，驅動程式或資料來源必須移除 null 結束的字元重組程序的一部分。  
  
7.  呼叫**SQLParamData**一次，以指示它已傳送所有參數的資料。 如果有任何資料在執行中參數的資料尚未傳送，驅動程式會傳回 SQL_NEED_DATA 和識別的下一個參數; 的值應用程式會傳回至步驟 6。 如果資料已傳送的所有資料在執行中參數，則會執行陳述式。 **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回任何傳回值或診斷， **SQLExecute**或**SQLExecDirect**可以傳回。  
  
 之後**SQLExecute**或**SQLExecDirect**傳回 SQL_NEED_DATA 和陳述式的最後一個資料執行參數已完全傳送資料之前，是在需要的資料狀態。 陳述式需要資料的狀態時，應用程式可以呼叫只**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函式會傳回 SQLSTATE HY010 （函數順序錯誤）。 呼叫**SQLCancel**取消執行陳述式並傳回其先前的狀態。 如需詳細資訊，請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需在執行階段傳送資料的範例，請參閱[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函式描述。

