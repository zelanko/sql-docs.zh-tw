---
title: SQLBindCol | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 407b20bfee027bd044993296894560e17e0f523b
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  一般的規則，請考量使用的含意**SQLBindCol**造成資料轉換。 例如，繫結轉換為用戶端處理序，所以擷取繫結至字元資料行的浮點值時，將會造成驅動程式在提取資料列時，於本機執行浮點對字元的轉換。 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 函數可將資料轉換的成本置於伺服器上。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以在單一陳述式執行中傳回多個結果資料列集。 每個結果集都必須個別繫結。 如需多個結果集繫結的詳細資訊，請參閱[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 開發人員可以繫結至資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-特有的 C 資料類型，使用*TargetType*值**SQL_C_BINARY**。 繫結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有之類型的資料行無法移植。 已定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有 ODBC C 資料類型符合 DB-Library 的類型定義，而移植應用程式的 DB-Library 開發人員可能會想要利用這項功能。  
  
 報告資料截斷是費時的程序的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。 您可以確保所有繫結的資料緩衝區都夠寬而足以傳回資料，藉此來避免資料遭到截斷。 如果是字元資料，當使用字串結束的預設驅動程式行為時，寬度應該包括字串結束字元的空格。 例如，繫結[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char(5)**陣列的五個字元的結果中擷取每個值的截斷的資料行。 將相同的資料行繫結至六個字元的陣列可藉由提供字元元素來儲存 Null 結束字元，以避免截斷的情況發生。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)可用來有效率地擷取長的字元和二進位資料，而不會截斷。  
  
 大數值資料類型，如果使用者提供的緩衝區不夠大，無法以保存整個值的資料行， **SQL_SUCCESS_WITH_INFO**傳回和 「 字串資料;右邊截斷 」 警告。 **StrLen_or_IndPtr**引數將會包含儲存在緩衝區內的字元/位元組數目。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol 對於增強型日期和時間功能的支援  
 結果資料行值的日期/時間類型轉換中所述[從 SQL 轉換成 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。請注意，若要擷取的時間和 datetimeoffset 資料行當做其對應的結構 (**SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT**)， *TargetType*必須指定為**SQL_C_DEFAULT**或**SQL_C_BINARY**。  
  
 如需詳細資訊，請參閱[日期和時間增強功能 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol 對於大型 CLR UDT 的支援  
 **SQLBindCol**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLBindCol 函數](http://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
