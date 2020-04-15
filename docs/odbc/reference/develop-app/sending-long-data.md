---
title: 傳送長資料 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304179"
---
# <a name="sending-long-data"></a>傳送長資料
DBMS 將*長數據*定義為特定大小的任意字元或二進位數據,例如 254 個字元。 可能無法將整個長數據項存儲在記憶體中,例如當專案表示長文本文檔或位圖時。 由於此類數據不能存儲在單個緩衝區中,因此在執行語句時,數據源會將其發送到**SQLPutData**的部件中的驅動程式。 在執行時傳送資料的參數稱為*執行時的資料參數*。  
  
> [!NOTE]  
>  應用程序實際上可以使用**SQLPutData**在執行時發送任何類型的數據,儘管只能分批發送字元和二進位數據。 但是,如果資料足夠小,可以容納單個緩衝區,則通常沒有理由使用**SQLPutData**。 綁定緩衝區並讓驅動程式從緩衝區檢索數據要容易得多。  
  
 在執行時傳送資料,應用程式執行以下操作:  
  
1.  傳遞一個 32 位值,該值標識**SQLBind 參數**中的*參數ValuePtr*參數中的參數,而不是傳遞緩衝區的位址。 驅動程式不分析此值。 稍後將返回到應用程式,因此對應用程式來說應有一些意義。 例如,它可能是參數的數量或包含數據的檔的句柄。  
  
2.  在**SQLBind 參數***的StrLen_or_IndPtr*參數中傳遞長度/指示器緩衝區的位址。  
  
3.  將SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果儲存在長度/指示器緩衝區中。 這兩個值都向驅動程式指示參數的數據將與**SQLPutData**一起發送。 SQL_LEN_DATA_AT_EXEC(*長度*)用於將長數據發送到數據源時,數據源需要知道將發送多少位元組的長數據,以便它可以預分配空間。 要確定資料來源是否需要此值,應用程式使用SQL_NEED_LONG_DATA_LEN選項調用**SQLGetInfo。** 所有驅動程式都必須支援此宏;所有驅動程式都必須支援此宏。如果數據源不需要位元組長度,驅動程式可以忽略它。  
  
4.  呼叫**SQLExecute**或**SQLExecDirect**。 驅動程序發現長度/指示器緩衝區包含值SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果,並返回SQL_NEED_DATA作為函數的返回值。  
  
5.  調用**SQLParamData**以回應SQL_NEED_DATA返回值。 如果需要發送長數據 **,SQLParamData**將返回SQL_NEED_DATA。 在*ValuePtrPtr*參數指向的緩衝區中,驅動程式返回標識執行時數據參數的值。 如果有多個執行時的數據參數,則應用程式必須使用此值來確定要為其發送數據的參數;驅動程式不需要按任何特定順序請求數據執行時參數的數據。  
  
6.  呼叫**SQLPutData**將參數資料傳送到驅動程式。 如果參數數據不適合單個緩衝區(與長數據通常的情況一樣),應用程式將重複調用 SQLPutData 以零件發送數據;如果參數數據不適合單個緩衝區,則應用程式將重複調用 SQLPutData 以發送部分數據;如果參數數據不適合,則調用**SQLPutData**以部分發送數據。由驅動程式和數據源重新組合數據。 如果應用程式傳遞 null 終止字串資料,驅動程式或數據源必須刪除 null 終止字元作為重新組裝過程的一部分。  
  
7.  再次調用**SQLParamData**以指示它已發送了參數的所有數據。 如果有任何未發送數據執行時的數據參數,驅動程式將返回SQL_NEED_DATA和標識下一個參數的值;應用程式返回到步驟 6。 如果已為執行時的所有資料參數發送數據,則執行語句。 **SQLParamData**傳回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,並可以返回 SQLExecute 或**SQLExecDirect**可以返回的**SQLExecDirect**任何返回值或診斷。  
  
 **在 SQLExecute**或**SQLExecDirect**傳回SQL_NEED_DATA後,在為上次執行時的數據完全發送數據之前,該語句處於「需要數據」 狀態。 當語句處於「需要數據」狀態時,應用程式只能調用 SQLPutData、SQLParamData、SQLCancel、SQLGetDiagField 或**SQLGetDiagRec;** **SQLPutData** **SQLParamData** **SQLCancel** **SQLGetDiagField**所有其他函數返回 SQLSTATE HY010(函數序列錯誤)。 調用**SQLCancel**會取消語句的執行並將其返回到其以前的狀態。 關於詳細資訊,請參閱附錄[B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有關在執行時發送數據的範例,請參閱[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函數說明。
