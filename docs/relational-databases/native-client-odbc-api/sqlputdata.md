---
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
ms.openlocfilehash: e063d1053d8a6e5e10a1234d33893adf27fbc3ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302339"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當您使用 SQLPutData 來傳送超過65535個位元組的資料（適用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]于 4.21 a）或 400 KB 的資料（適用于 SQL Server 6.0 和更新版本） SQL_LONGVARCHAR （**text**）、SQL_WLONGVARCHAR （**Ntext**）或 SQL_LONGVARBINARY （**image**）資料行時，適用下列限制：  
  
-   參考的參數可以是 INSERT 語句中的*insert_value* 。  
  
-   參考的參數可以是 UPDATE 語句的 SET 子句中的*運算式*。  
  
 在使用6.5 或更早版本時，取消將區塊中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供給執行之伺服器的 SQLPutData 呼叫順序，會造成資料行值的部分更新。 呼叫 SQLCancel 時所參考的**text**、 **Ntext**或**image**資料行，會設定為中繼預留位置值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版和更早版本。  
  
## <a name="diagnostics"></a>診斷  
 有一個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]適用于 SQLPutData 的原生用戶端特定 SQLSTATE：  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|22026|字串資料，長度不符|如果應用程式已指定要傳送的資料長度（以位元組為單位），例如，使用 SQL_LEN_DATA_AT_EXEC （*n*），其中*n*大於0，則應用程式透過 SQLPutData 所提供的位元組總數必須符合指定的長度。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 和資料表值參數  
 當使用具有資料表值參數的變數資料列系結時，應用程式會使用 SQLPutData。 *StrLen_Or_Ind*參數表示已準備好讓驅動程式收集資料表值參數資料的下一個或多個資料列的資料，或沒有其他可用的資料列：  
  
-   大於 0 的值表示有下一組資料列值。  
  
-   0 這個值表示沒有其他要傳送的資料列。  
  
-   小於 0 的任何值都是錯誤，而且會記錄 SQLState HY090 以及訊息「無效的字串或緩衝區長度」的診斷記錄。  
  
 *DataPtr*參數會被忽略，但必須設定為非 Null 值。 如需詳細資訊，請參閱在系結[和資料表值參數和資料行中的資料傳輸](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)中的變數 TVP 資料列系結一節。  
  
 如果*StrLen_Or_Ind*具有 SQL_DEFAULT_PARAM 以外的任何值，或介於0與 SQL_PARAMSET_SIZE 之間的數位（也就是 SQLBindParameter 的*ColumnSize*參數），就會發生錯誤。 此錯誤會使 SQLPutData 傳回 SQL_ERROR：SQLSTATE=HY090，表示「無效的字串或緩衝區長度」。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLPutData 支援  
 日期/時間類型的參數值會依照[從 C 轉換成 SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)中所述的方式進行轉換。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLPutData 支援  
 **SQLPutData**支援大型 CLR 使用者定義型別（udt）。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLPutData 函式](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
