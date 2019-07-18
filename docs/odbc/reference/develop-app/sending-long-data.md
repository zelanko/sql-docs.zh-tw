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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: acb4ff1637c1530527af88affaf437334596016b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094345"
---
# <a name="sending-long-data"></a>傳送長資料
定義 Dbms*長資料*為任何字元或二進位資料超過特定大小，例如 254 個字元。 它可能無法儲存在記憶體中，例如當項目所表示的長文字文件或點陣圖的長資料的整個項目。 因為這類資料無法儲存在單一緩衝區中，資料來源就會將它傳送至使用組件中驅動程式**SQLPutData**陳述式執行時。 參數的資料會在執行階段傳送稱為*資料在執行中參數*。  
  
> [!NOTE]  
>  在執行階段使用中應用程式可以確實傳送任何資料型別**SQLPutData**，不過，在組件，則會傳送只字元和二進位資料。 不過，如果資料夠小，無法放入單一緩衝區中，有通常是使用沒有理由**SQLPutData**。 很容易繫結緩衝區，並讓驅動程式從緩衝區中擷取資料。  
  
 若要在執行階段傳送資料，應用程式會執行下列動作：  
  
1.  將 32 位元值，識別中的參數傳遞*ParameterValuePtr*中的引數**SQLBindParameter**而不是傳遞緩衝區的位址。 這個值就不會分析驅動程式。 它會傳回至更新版本中，應用程式，所以它應該會有意義的應用程式。 比方說，它可能是參數的數字或包含資料的檔案控制代碼。  
  
2.  傳遞的長度/指標緩衝區的位址*StrLen_or_IndPtr*引數**SQLBindParameter**。  
  
3.  儲存 SQL_DATA_AT_EXEC 或結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 之長度/指標緩衝區中的巨集。 這些值都表示驅動程式的參數的資料將會傳送具有**SQLPutData**。 SQL_LEN_DATA_AT_EXEC (*長度*) 長資料傳送至資料來源，必須知道會傳送多少個位元組的 long 資料，以便讓它可以預先配置空間時使用。 若要判斷資料來源需要此值，是否應用程式會呼叫**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 選項。 所有驅動程式必須支援這個巨集;如果資料來源不需要的位元組長度，此驅動程式可以忽略它。  
  
4.  呼叫**SQLExecute**或是**SQLExecDirect**。 驅動程式可讓您探索長度/指標緩衝區包含值 SQL_DATA_AT_EXEC 或結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集，並傳回 SQL_NEED_DATA 函式的傳回值。  
  
5.  呼叫**SQLParamData** SQL_NEED_DATA 的回應中傳回的值。 如果需要傳送長資料**SQLParamData**會傳回 SQL_NEED_DATA。 中所指向的緩衝區*ValuePtrPtr*引數，驅動程式會傳回識別資料在執行中參數的值。 如果有一個以上的資料在執行中參數，應用程式就必須使用此值來判斷哪些參數來傳送資料;驅動程式不需要要求任何特定順序中的資料在執行參數的資料。  
  
6.  呼叫**SQLPutData**將參數資料傳送給驅動程式。 如果參數資料無法容納到單一的緩衝區，通常就是 long 資料的情況，應用程式會呼叫**SQLPutData**不斷地將資料傳送部分; 是由驅動程式和資料來源來重組資料。 如果應用程式傳遞 null 結束的字串資料，驅動程式或資料來源必須移除 null 終止的字元重組程序的一部分。  
  
7.  呼叫**SQLParamData**以表示它已傳送所有參數的資料。 如果有任何資料在執行中參數的資料尚未傳送，驅動程式會傳回 SQL_NEED_DATA 和識別下一個參數; 的值應用程式會傳回至步驟 6。 如果資料已傳送的所有資料在執行中參數，則會執行陳述式。 **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回任何傳回值或診斷所**SQLExecute**或是**SQLExecDirect**可以傳回。  
  
 在後**SQLExecute**或是**SQLExecDirect**會傳回 SQL_NEED_DATA 且資料已完全傳送最後一個資料在執行中參數之前，陳述式中需要的資料狀態。 應用程式需要的資料狀態的陳述式時，可以只呼叫**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函式會傳回 SQLSTATE HY010 （函數順序錯誤）。 呼叫**SQLCancel**取消執行陳述式，並傳回其先前的狀態。 如需詳細資訊，請參閱[附錄 b:狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需在執行階段傳送資料的範例，請參閱[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函式描述。
