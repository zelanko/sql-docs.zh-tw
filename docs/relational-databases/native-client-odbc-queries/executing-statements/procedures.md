---
title: 程式 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 59d971f4d835470924874b0a08a648d36d98c0f9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297908"
---
# <a name="procedures"></a>程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  預存程序是包含一個或多個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的先行編譯可執行物件。 預存程序可以有輸入和輸出參數，也可以輸出整數傳回碼。 應用程式可以使用目錄函數來列舉可用的預存程序。  
  
 目標為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC 應用程式僅能使用直接執行來呼叫預存程序。 當連線到的早期版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 本機用戶端 ODBC 驅動程式透過建立暫存記憶體來實現[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360),然後在**SQLExecute**上調用該過程。 它增加了開銷,讓**SQLPrepare**創建暫存記憶體,該過程僅調用目標儲存過程,而不是直接執行目標儲存過程。 即使在連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時，跨網路準備呼叫都需要額外的往返，而且需要建立只呼叫預存程序執行計畫的執行計畫。  
  
 執行預存程序時，ODBC 應用程式應該會使用 ODBC CALL 語法。 使用 ODBC CALL 語法時，系統會最佳化驅動程式，使用遠端程序呼叫機制來呼叫程序。 這比將 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 陳述式傳送到伺服器所使用的機制更有效率。  
  
 有關詳細資訊,請參閱[執行儲存過程](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)。  
  
## <a name="see-also"></a>另請參閱  
 [執行宣告&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
