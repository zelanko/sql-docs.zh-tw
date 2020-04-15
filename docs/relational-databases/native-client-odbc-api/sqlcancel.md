---
title: SQL取消 |微軟文件
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
ms.openlocfilehash: 2db2c4b66940a81dd65064ee730cd683e2206a58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302633"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主題指出,在 ODBC 2.x 中,如果應用程式在未對語句執行處理時調用**SQLCancel,****則 SQLCancel**具有與**SQLFreeStmt**與**使用SQL_CLOSE**選項相同的效果;此行為僅針對完整性而定義,應用程式應調用**SQLFreeStmt**或**SQLCloseCursor**來關閉游標。 但是,即使本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客戶端應用程式將 ODBC API 版本設定為 3.5.x 或更高版本 **,SQLCancel**函數也將使用 ODBC 2.x 行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQL取消](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
