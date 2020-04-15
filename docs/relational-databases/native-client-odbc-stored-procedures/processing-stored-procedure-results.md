---
title: 處理儲存過程結果 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d246756161e129f3f1d4c6efe5192ce39ff777d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304534"
---
# <a name="processing-stored-procedure-results"></a>處理預存程序結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序有四個用於傳回資料的機制：  
  
-   程序中的每個 SELECT 陳述式都會產生一個結果集。  
  
-   程序可以透過輸出參數傳回資料。  
  
-   資料指標輸出參數可以傳回 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標。  
  
-   程序可以有一個整數的傳回碼。  
  
 應用程式必須能夠處理預存程序中的所有這些輸出。 CALL 或 EXECUTE 陳述式應該包含適用於傳回碼和輸出參數的參數標記。 使用[SQLBind 參數](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)將它們全部綁定為輸出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]參數, 本機用戶端 ODBC 驅動程式將輸出值傳輸到綁定變數。 輸出參數和返回代碼是返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]給客戶端的最後一項。在[SQLMore 結果](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)返回SQL_NO_DATA之前,它們不會返回到應用程式。  
  
 ODBC 不支援繫結 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標參數。 由於所有輸出參數都必須在執行程序之前進行繫結，因此，ODBC 應用程式無法呼叫包含輸出資料指標參數的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
