---
title: SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05b4f3208b13f1f13f584628e9d495ff1cbf4060
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789410"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主題指出，在 ODBC 2.x 中，如果應用程式在未于語句上進行任何處理時呼叫**SQLCancel** ， **SQLCancel**與**SQLFreeStmt**與**SQL_CLOSE**選項的效果相同。此行為僅針對完整性而定義，而應用程式應該呼叫**SQLFreeStmt**或**SQLCloseCursor**來關閉資料指標。 但是，即使您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 應用程式將 ODBC API 版本設定為 3.5. x 或之後， **SQLCancel**函數還是會使用 odbc 2.x 行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
