---
title: SQLPutData | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1c362a9d1797a5b770aaabf6dbd19761033545e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682886"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用 SQLPutData 傳送 65,535 個位元組以上的資料時，適用下列限制 (如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.21a 版) 或 400 KB 的資料 （適用於 SQL Server 6.0 版和更新版本)，針對 SQL_LONGVARCHAR (**文字**)、 SQL_WLONGVARCHAR(**ntext**) 或 SQL_LONGVARBINARY (**映像**) 資料行：  
  
-   參考的參數可以是*insert_value* INSERT 陳述式中。  
  
-   參考的參數可以是*運算式*UPDATE 陳述式的 SET 子句中。  
  
 取消一系列的可執行的伺服器的區塊中的資料 SQLPutData 呼叫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 6.5 或更早版本時，會導致部分更新的資料行的值。 **文字**， **ntext**，或**映像**SQLCancel 呼叫時所參考的資料行設為中繼預留位置的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版和更早版本。  
  
## <a name="diagnostics"></a>診斷  
 有一個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 專屬 SQLSTATE 的 SQLPutData:  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|22026|字串資料，長度不符|如果要傳送的位元組資料長度已指定應用程式，比方說，使用 SQL_LEN_DATA_AT_EXEC (*n*)， *n*大於 0，應用程式透過所指定的位元組總數SQLPutData 必須符合指定的長度。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 和資料表值參數  
 使用資料表值參數使用變數的資料列繫結時，應用程式會使用 SQLPutData。 *Strlen_or_ind&lt*參數表示收集下一個資料列或資料表值參數資料列的資料驅動程式準備就緒或沒有其他資料列有可供使用：  
  
-   大於 0 的值表示有下一組資料列值。  
  
-   0 這個值表示沒有其他要傳送的資料列。  
  
-   小於 0 的任何值都是錯誤，而且會記錄 SQLState HY090 以及訊息「無效的字串或緩衝區長度」的診斷記錄。  
  
 *DataPtr*參數會被忽略，但必須設定為非 NULL 值。 如需詳細資訊，請參閱節變數 TVP 資料列中的繫結[繫結和 Data Transfer of Table-Valued 參數和資料行值](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如果*Strlen_or_ind&lt* SQL_DEFAULT_PARAM 或介於 0 和 SQL_PARAMSET_SIZE 以外的任何值 (亦即*ColumnSize* SQLBindParameter 參數)，就會發生錯誤。 此錯誤會使 SQLPutData 傳回 SQL_ERROR：SQLSTATE=HY090，表示「無效的字串或緩衝區長度」。  
  
 如需有關資料表值參數的詳細資訊，請參閱 < [Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLPutData 支援  
 參數值的日期/時間類型轉換中所述[從 C 轉換成 SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLPutData 支援  
 **SQLPutData**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱 < [Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLPutData 函數](http://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
