---
title: 如何：使用 SQLSRV 驅動程式指定參數方向 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 33613a90ee21069b2ef7d2f9908ed13bd4f040e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799679"
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式指定參數方向
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題說明在呼叫預存程序時，如何使用 SQLSRV 驅動程式來指定參數方向。 參數方向是在您建構傳遞至 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 的參數陣列 (步驟 3) 時指定。  
  
### <a name="to-specify-parameter-direction"></a>指定參數方向  
  
1.  定義會呼叫預存程序的 Transact-SQL 查詢。 請使用問號 (?) 來取代要傳遞至預存程序的參數。 例如，下列字串會呼叫可接受兩個參數的預存程序 (UpdateVacationHours)：  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > 使用標準語法呼叫預存程序，是建議的做法。 如需標準語法的詳細資訊，請參閱[呼叫預存程序](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)。  
  
2.  初始化或更新對應至 Transact-SQL 查詢中預留位置的 PHP 變數。 例如，下列程式碼會為 UpdateVacationHours 預存程序初始化兩個參數：  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > 初始化或更新為 **null**、 **DateTime**或資料流類型的變數，無法作為輸出參數。  
  
3.  使用步驟 2 中的 PHP 變數來建立或更新依序對應至 Transact-SQL 字串中參數預留位置的參數值陣列。 指定陣列中每個參數的方向。 每個參數的方向可由下列兩種方式之一來決定：根據預設 (適用於輸入參數)，或使用 **SQLSRV_PARAM_\*** 常數 (適用於輸出和雙向參數)。 例如，下列程式碼會將 *$employeeId* 參數指定為輸入參數，並將 *$usedVacationHours* 參數指定為雙向參數：  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    為了大致了解指定參數方向的語法，我們假設 *$var1*、 *$var2*和 *$var3* 分別對應至輸入、輸出和雙向參數。 您可以透過下列其中一種方式來指定參數方向：  
  
    -   隱含地指定輸入參數、明確地指定輸出參數及雙向參數：  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   明確地指定輸入參數、輸出參數及雙向參數：  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 執行查詢，或使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 和 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 來執行。 例如，下列程式碼會使用連接 *$conn* ，執行在 *$params* 中指定了參數值的查詢 *$tsql*：  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>另請參閱  
[如何：使用 SQLSRV 驅動程式擷取輸出參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[如何：使用 SQLSRV 驅動程式擷取輸入和輸出參數](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
