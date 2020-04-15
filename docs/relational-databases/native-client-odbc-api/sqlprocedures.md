---
title: SQL 程式 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14ff76504c9a36657be60ba4855cf252474071d7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302356"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQL過程**報告結果集列PROCEDURE_TYPESQL_PT_FUNCTION。  
  
 **SQL過程**傳回SQL_SUCCESS*目錄名稱、架構名稱*或*ProcName*參數是否存在值。 當在這些參數中使用無效值時 **,SQLFetch**將返回SQL_NO_DATA。  
  
 **SQL過程**可以在靜態伺服器游標上執行。 嘗試在可上升(動態或鍵集)游標上執行**SQL 過程**將返回SQL_SUCCESS_WITH_INFO,指示游標類型已更改。  
  
 **SQL程式**傳回有關名稱與*ProcName*匹配且可以由目前的使用者執行或目前使用者已被授予「檢視定義」許可權的任何過程的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQL程式函數](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
