---
description: SQLPutData
title: SQLPutData |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42323e6fbf35ddb6093ac4e764e81e7f0274cbb2
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867481"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當您使用 SQLPutData 將65535個以上的資料 (傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的) 或 400 KB 的資料 (適用 6.0 SQL Server 于) SQL_LONGVARCHAR **文字** (、) SQL_WLONGVARCHAR **Ntext** (或) SQL_LONGVARBINARY **影像** (資料行時，適用下列限制：  
  
-   在 INSERT 語句中，參考的參數可以是 *insert_value* 。  
  
-   參考的參數可以是 UPDATE 語句的 SET 子句中的 *運算式* 。  
  
 在使用6.5 版或更早版本時，取消將區塊中的資料提供給執行之伺服器的一連串 SQLPutData 呼叫， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會造成資料行值的部分更新。 呼叫 SQLCancel 時參考的 **text**、 **Ntext**或 **image** 資料行，會設定為中繼預留位置值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版和更早版本。  
  
## <a name="diagnostics"></a>診斷  
 有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 適用于 SQLPutData 的原生用戶端專用 SQLSTATE：  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|22026|字串資料，長度不符|如果應用程式已經指定要傳送的位元組長度（以位元組為單位），例如 SQL_LEN_DATA_AT_EXEC (*n*) 其中 *n* 大於0，則應用程式透過 SQLPutData 提供的位元組總數必須符合指定的長度。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 和資料表值參數  
 使用具有資料表值參數的變數資料列系結時，應用程式會使用 SQLPutData。 *StrLen_Or_Ind*參數表示它已準備好供驅動程式收集資料表值參數資料的下一個資料列或資料列的資料，或沒有其他可用的資料列：  
  
-   大於 0 的值表示有下一組資料列值。  
  
-   0 這個值表示沒有其他要傳送的資料列。  
  
-   小於 0 的任何值都是錯誤，而且會記錄 SQLState HY090 以及訊息「無效的字串或緩衝區長度」的診斷記錄。  
  
 *DataPtr*參數會被忽略，但必須設定為非 Null 值。 如需詳細資訊，請參閱 [Table-Valued 參數和資料行值之系結和資料傳輸](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)中的變數 TVP 資料列系結一節。  
  
 如果 *StrLen_Or_Ind* 具有 SQL_DEFAULT_PARAM 以外的任何值或介於0和 SQL_PARAMSET_SIZE 之間的數位 (也就是 SQLBindParameter) 的 *ColumnSize* 參數，則會是錯誤。 此錯誤會使 SQLPutData 傳回 SQL_ERROR：SQLSTATE=HY090，表示「無效的字串或緩衝區長度」。  
  
 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLPutData 支援  
 日期/時間類型的參數值會如 [從 C 轉換成 SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)所述進行轉換。  
  
 如需詳細資訊，請參閱 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLPutData 支援  
 **SQLPutData** 支援)  (udt 的大型 CLR 使用者自訂類型。 如需詳細資訊，請參閱 [&#40;ODBC&#41;的大型 CLR User-Defined 類型 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLPutData 函式](../../odbc/reference/syntax/sqlputdata-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
