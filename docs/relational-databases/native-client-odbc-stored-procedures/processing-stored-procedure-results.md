---
title: 處理預存程式結果 |Microsoft Docs
description: 瞭解 SQL Server 預存程式用來將資料傳回給應用程式的機制。 應用程式必須能夠處理所有這些類型。
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1e01b61f3eb19b06b9f61653fe839818e52702d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97437436"
---
# <a name="processing-stored-procedure-results"></a>處理預存程序結果
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序有四個用於傳回資料的機制：  
  
-   程序中的每個 SELECT 陳述式都會產生一個結果集。  
  
-   程序可以透過輸出參數傳回資料。  
  
-   資料指標輸出參數可以傳回 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標。  
  
-   程序可以有一個整數的傳回碼。  
  
 應用程式必須能夠處理預存程序中的所有這些輸出。 CALL 或 EXECUTE 陳述式應該包含適用於傳回碼和輸出參數的參數標記。 使用 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 將它們全部系結為輸出參數，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會將輸出值傳送至系結變數。 輸出參數和傳回碼是最後一個傳回給用戶端的專案 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; 除非 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 傳回 SQL_NO_DATA，否則它們不會傳回至應用程式。  
  
 ODBC 不支援繫結 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標參數。 由於所有輸出參數都必須在執行程序之前進行繫結，因此，ODBC 應用程式無法呼叫包含輸出資料指標參數的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
