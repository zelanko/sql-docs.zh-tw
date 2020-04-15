---
title: SQLPutData |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302339"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當使用 SQLPutData 送出超過 65,535[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]位元組資料( 對於版本 4.21a)或 400 KB 的資料(對於 SQL Server 版本 6.0 及更高版本)時,以下限制適用於**ntext**SQL_LONGVARCHAR(**text**)、SQL_WLONGVARCHAR(ntext)或SQL_LONGVARBINARY(**圖像**)列:  
  
-   引用的參數可以是 INSERT 語句中*insert_value。*  
  
-   參考的參數可以是 UPDATE 語句的 SET 子句中的*表示式*。  
  
 取消一系列 SQLPutData 調用,這些調用在塊中向正在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]運行的 伺服器提供數據,會導致在使用版本 6.5 或更早版本時部分更新列的值。 呼叫 SQLCancel 時引用**的文字****、ntext**或**影像**列設定為中間占位符值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版和更早版本。  
  
## <a name="diagnostics"></a>診斷  
 SQLPutData[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有一個特定於本機客戶端的 SQLSTATE:  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|22026|字串資料，長度不符|如果要發送的數據長度(以位元組為單位)由應用程式指定,例如,SQL_LEN_DATA_AT_EXEC(n *)n大於**n*0,則應用程式通過 SQLPutData 給出的位元組總數必須與指定的長度匹配。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 和資料表值參數  
 當使用具有表值參數的變數行綁定時,應用程式使用 SQLPutData。 *StrLen_Or_Ind*參數指示驅動程式已準備好為表值參數資料的下一行或行收集資料,或者沒有更多的列可用:  
  
-   大於 0 的值表示有下一組資料列值。  
  
-   0 這個值表示沒有其他要傳送的資料列。  
  
-   小於 0 的任何值都是錯誤，而且會記錄 SQLState HY090 以及訊息「無效的字串或緩衝區長度」的診斷記錄。  
  
 *DataPtr*參數將被忽略,但必須設置為非 NULL 值。 有關詳細資訊,請參閱[表值參數和列值的綁定和數據傳輸](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)中變數 TVP 行綁定部分。  
  
 如果*StrLen_Or_Ind*具有SQL_DEFAULT_PARAM以外的任何值或介於 0 和SQL_PARAMSET_SIZE之間的數位(即 SQLBind 參數的*列大小*參數),則這是一個錯誤。 此錯誤會使 SQLPutData 傳回 SQL_ERROR：SQLSTATE=HY090，表示「無效的字串或緩衝區長度」。  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLPutData 支援  
 日期/時間類型的參數值將轉換,如從[C 到 SQL 的轉換](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)中所述。  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLPutData 支援  
 **SQLPutData**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLPutData 函數](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
