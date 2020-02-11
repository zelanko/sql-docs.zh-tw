---
title: SQLBindCol |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a92c95a67b6e9fd3d31917af4f5b7b19f4c613d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787788"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  作為一般規則，請考慮使用**SQLBindCol**來造成資料轉換的含意。 例如，繫結轉換為用戶端處理序，所以擷取繫結至字元資料行的浮點值時，將會造成驅動程式在提取資料列時，於本機執行浮點對字元的轉換。 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 函數可將資料轉換的成本置於伺服器上。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以在單一陳述式執行中傳回多個結果資料列集。 每個結果集都必須個別繫結。 如需多個結果集之系結的詳細資訊，請參閱[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 開發人員可以使用*TargetType*值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL_C_BINARY**，將資料行系結至特定的 C 資料類型。 繫結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有之類型的資料行無法移植。 已定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有 ODBC C 資料類型符合 DB-Library 的類型定義，而移植應用程式的 DB-Library 開發人員可能會想要利用這項功能。  
  
 報表資料截斷是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式的昂貴進程。 您可以確保所有繫結的資料緩衝區都夠寬而足以傳回資料，藉此來避免資料遭到截斷。 如果是字元資料，當使用字串結束的預設驅動程式行為時，寬度應該包括字串結束字元的空格。 例如，將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char （5）** 資料行系結至五個字元的陣列，會導致每個提取的值截斷。 將相同的資料行繫結至六個字元的陣列可藉由提供字元元素來儲存 Null 結束字元，以避免截斷的情況發生。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)可以用來有效率地抓取長字元和二進位資料，而不會進行截斷。  
  
 對於大數值資料類型，如果使用者提供的緩衝區不夠大，無法保存資料行的整個值，則會傳回**SQL_SUCCESS_WITH_INFO** ，並將 "string data;右側截斷」警告。 **StrLen_or_IndPtr**引數會包含儲存在緩衝區中的字元/位元組數目。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol 對於增強型日期和時間功能的支援  
 日期/時間類型的結果資料行值會轉換，如[從 SQL 轉換為 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述。請注意，若要取出 time 和 datetimeoffset 資料行做為其對應的結構（**SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT**）， *TargetType*必須指定為**SQL_C_DEFAULT**或**SQL_C_BINARY**。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol 對於大型 CLR UDT 的支援  
 **SQLBindCol**支援大型 CLR 使用者定義型別（udt）。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLBindCol 函式](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
