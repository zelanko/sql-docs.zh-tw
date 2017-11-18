---
title: "如何： 使用 SQLSRV 驅動程式指定參數方向 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 404054a7d2fea19c6e8d0739f4497054ca8d3f2b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式指定參數方向
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題說明在呼叫預存程序時，如何使用 SQLSRV 驅動程式來指定參數方向。 請注意當您建構參數時，會指定參數方向陣列 （步驟 3） 傳遞至[sqlsrv_query](../../connect/php/sqlsrv-query.md)或[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)。  
  
### <a name="to-specify-parameter-direction"></a>指定參數方向  
  
1.  定義會呼叫預存程序的 Transact-SQL 查詢。 請使用問號 (?) 來取代要傳遞至預存程序的參數。 例如，下列字串會呼叫可接受兩個參數的預存程序 (UpdateVacationHours)：  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > 使用標準語法呼叫預存程序，是建議的做法。 如需關於標準語法的詳細資訊，請參閱 [呼叫預存程序](http://go.microsoft.com/fwlink/?linkid=119517)。  
  
2.  初始化或更新對應至 Transact-SQL 查詢中預留位置的 PHP 變數。 例如，下列程式碼會為 UpdateVacationHours 預存程序初始化兩個參數：  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > 初始化或更新為 **null**、 **DateTime**或資料流類型的變數，無法作為輸出參數。  
  
3.  使用步驟 2 中的 PHP 變數來建立或更新依序對應至 Transact-SQL 字串中參數預留位置的參數值陣列。 指定陣列中每個參數的方向。 每個參數的方向由決定在兩種方式之一： 預設 （適用於輸入參數） 或使用**SQLSRV_PARAM_\*** 常數 （適用於輸出和雙向參數）。 例如，下列程式碼會將 *$employeeId* 參數指定為輸入參數，並將 *$usedVacationHours* 參數指定為雙向參數：  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    為了大致了解指定參數方向的語法，我們假設 *$var1*、 *$var2*和 *$var3* 分別對應至輸入、輸出和雙向參數。 您可以透過下列其中一種方式來指定參數方向：  
  
    -   隱含地指定輸入參數、明確指定輸出參數，以及明確指定雙向參數：  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   明確指定輸入參數、明確指定輸出參數，以及明確指定雙向參數：  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  執行與查詢[sqlsrv_query](../../connect/php/sqlsrv-query.md)或[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)和[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)。 例如，下列程式碼會使用連接 *$conn* ，執行在 *$params* 中指定了參數值的查詢 *$tsql*：  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>另請參閱  
[如何：使用 SQLSRV 驅動程式擷取輸出參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)  
[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  

