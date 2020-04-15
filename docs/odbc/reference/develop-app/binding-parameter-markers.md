---
title: 繫結參數標記 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be99bc884a8baa66f3d632ee4731985f0cc85732
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306389"
---
# <a name="binding-parameter-markers"></a>繫結參數標記
應用程式通過調用**SQLBind 參數**來綁定參數。 **SQLBind 參數**一次綁定一個參數。 使用它,應用程式指定以下內容:  
  
-   參數編號。 參數按 SQL 語句中增加參數順序進行編號,從數位 1 開始。 雖然指定高於 SQL 語句中的參數數的參數編號是合法的,但在執行語句時將忽略參數值。  
  
-   參數類型(輸入、輸入/輸出或輸出)。 除過程呼叫中的參數外,所有參數都是輸入參數。 有關詳細資訊,請參閱本部份後面的[程序參數](../../../odbc/reference/develop-app/procedure-parameters.md)。  
  
-   綁定到參數的變數的 C 資料類型、位址和位元組長度。 驅動程式必須能夠將數據從 C 資料類型轉換為 SQL 資料類型,否則將返回錯誤。 有關受支援的轉化清單,請參閱附錄 D:資料類型[中 將資料從 C 轉換為 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
-   參數本身的 SQL 資料類型、精度和縮放。  
  
-   長度/指示器緩衝區的位址。 它提供二進位或字元資料的位元組長度,指定資料為 NULL,或指定數據將與**SQLPutData**一起發送。 關於詳細資訊,請參閱[使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 例如,以下代碼將*銷售人員*和*庫斯特ID*綁定到銷售人員和庫斯特ID列的參數。 由於*SalesPerson*包含字元數據(即可變長度),因此代碼指定*SalesPerson* (11) 的位元組長度,並將*SalesPersonLenOrInd*綁定以包含*SalesPerson*中數據的位元組長度。 *對於 CustID*來說,此資訊是不需要的,因為它包含整數數據,數據長度固定。  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 調用**SQLBind 參數**時,驅動程式將此資訊存儲在語句的結構中。 執行敘述時,它使用資訊檢索參數數據並將其發送到資料來源。  
  
> [!NOTE]  
>  在 ODBC 1.0 中,參數與**SQLSetParam**綁定。 驅動程式管理器對應**SQLSetParam**和**SQLBind 參數**之間的調用,具體取決於應用程式和驅動程式使用的 ODBC 版本。
