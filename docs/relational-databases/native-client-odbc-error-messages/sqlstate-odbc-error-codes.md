---
title: SQLSTATE （ODBC 錯誤碼） |Microsoft Docs
description: 當 SQL Server ODBC 驅動程式將預存程式當做遠端預存程式來執行時，此程式可以有整數傳回碼和輸出參數。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4efb5bae1383e64bf8b2d13c7f667183e617689d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787962"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  SQLSTATE 會提供警告或錯誤原因的詳細資訊。 對於偵測到並傳回的資料來源發生的錯誤 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會將傳回的原生錯誤號碼對應至適當的 SQLSTATE。 如果原生錯誤號碼沒有要對應的 ODBC 錯誤碼， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會傳回 SQLSTATE 42000 （「語法錯誤或存取違規」）。 對於驅動程式所偵測到的錯誤， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會產生適當的 SQLSTATE。  
  
 如需有關狀態錯誤碼的詳細資訊，請查看下列主題：  
  
-   [附錄 A：ODBC 錯誤碼](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 對應](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
