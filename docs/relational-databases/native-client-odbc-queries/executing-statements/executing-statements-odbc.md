---
title: 執行語句（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efd0b9ba46975512491dadccb5a44940af52ec28
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73791031"
---
# <a name="executing-statements-odbc"></a>執行陳述式 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式提供各種方式來執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中的 SQL 語句：  
  
-   直接執行  
  
-   準備執行  
  
 直接執行牽涉到建立包含 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句的字元字串，並使用**SQLExecDirect**函數提交它來執行。 準備執行則包括建立含有 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的字元字串，然後在兩個階段中執行此字串。 第一個階段會使用[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360)函數來剖析和編譯 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]中語句的執行計畫。 第二個階段會使用**SQLExecute**函數來執行先前已備妥的執行計畫。 這樣會省下每次執行時的剖析和編譯負擔。 應用程式通常會使用備妥的執行來重複執行相同且參數化的 SQL 陳述式。  
  
 直接和準備執行都可以執行單一 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式或 SQL 陳述式批次，也可以呼叫預存程序。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [直接執行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [備妥的執行](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [程序](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [陳述式的批次](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [ISO 選項的作用](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
