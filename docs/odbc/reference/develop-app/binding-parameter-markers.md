---
description: 繫結參數標記
title: 系結參數標記 |Microsoft Docs
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
ms.openlocfilehash: 259faf84e0388f74662471583657da1fd95bb007
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476850"
---
# <a name="binding-parameter-markers"></a>繫結參數標記
應用程式會藉由呼叫 **SQLBindParameter**來系結參數。 **SQLBindParameter** 一次系結一個參數。 使用此應用程式時，應用程式會指定下列各項：  
  
-   參數編號。 參數的編號是 SQL 語句中遞增的參數順序，從數位1開始。 雖然指定的參數編號高於 SQL 語句中的參數數目，但在執行語句時，將會忽略參數值。  
  
-   參數類型 (輸入、輸入/輸出或輸出) 。 除了程序呼叫中的參數，所有參數都是輸入參數。 如需詳細資訊，請參閱本節稍後的程式 [參數](../../../odbc/reference/develop-app/procedure-parameters.md)。  
  
-   系結至參數之變數的 C 資料類型、位址和位元組長度。 驅動程式必須能夠將 C 資料類型的資料轉換成 SQL 資料類型，否則會傳回錯誤。 如需支援的轉換清單，請參閱附錄 D：資料類型中的 [將資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 。  
  
-   參數本身的 SQL 資料類型、精確度和小數位數。  
  
-   長度/指標緩衝區的位址。 它會提供二進位或字元資料的位元組長度，指定資料為 Null，或指定資料將會以 **SQLPutData**傳送。 如需詳細資訊，請參閱 [使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 例如，下列程式碼會將 *銷售人員* 和 *CustID* 系結至銷售人員和 CustID 資料行的參數。 因為 *銷售人員* 包含長度可變的字元資料，所以程式碼會指定 *銷售人員* (11) 的位元組長度，並系結 *SalesPersonLenOrInd* 以包含 *銷售人員*資料的位元組長度。 *CustID*不需要此資訊，因為它包含長度固定的整數資料。  
  
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
  
 當呼叫 **SQLBindParameter** 時，驅動程式會將這項資訊儲存在語句的結構中。 當語句執行時，它會使用此資訊來取出參數資料，並將其傳送至資料來源。  
  
> [!NOTE]  
>  在 ODBC 1.0 中，參數已與 **SQLSetParam**系結。 驅動程式管理員會根據應用程式和驅動程式所使用的 ODBC 版本，對應 **SQLSetParam** 與 **SQLBindParameter**之間的呼叫。
