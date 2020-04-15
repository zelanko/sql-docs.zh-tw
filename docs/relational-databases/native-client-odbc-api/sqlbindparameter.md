---
title: SQLBind參數 |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74122d531eba1f714e16c168838ee1653a8f1293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302679"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當用於為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式提供資料時 **,SQLBindParameter**可以消除資料轉換的負擔,從而顯著提升應用程式的用戶端和伺服器元件的性能。 其他優點包括插入或更新近似的數值資料類型時，降低有效位數的損失。  
  
> [!NOTE]  
>  將**char**和**wchar**類型資料插入影像列時,將使用傳入的資料大小,而不是轉換為二進位格式後的資料大小。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式在任何參數陣列的單一陣列元素上碰到錯誤，驅動程式會繼續執行其餘陣列元素的陳述式。 如果應用程式已經繫結陳述式的參數狀態元素陣列，可以從陣列判斷產生錯誤的參數資料列。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式，指定繫結輸入參數時的 SQL_PARAM_INPUT。 繫結使用 OUTPUT 關鍵字定義的預存程序參數時，只會指定 SQL_PARAM_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT。  
  
 如果綁定參數陣列的陣列元素[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]導致語句執行錯誤,[則 SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)對於本機用戶端 ODBC 驅動程式不可靠。 ODBC 陳述式屬性 SQL_ATTR_PARAMS_PROCESSED_PTR 會報告錯誤發生前處理的資料列數目。 接著，如果需要，此應用程式可以周遊其參數狀態陣列以探索成功執行的陳述式數目。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 字元類型的繫結參數  
 如果傳入的 SQL 資料類型是字元類型,則*列大小*以字元(而不是位元組為單位)。 如果位元組中的數據字串的長度大於 8000,則*列大小*應設置為**SQL_SS_LENGTH_UNLIMITED,** 指示 SQL 類型的大小沒有限制。  
  
 例如,如果 SQL 資料類型為**SQL_WVARCHAR**,*則列大小*不應大於 4000。 如果實際數據長度大於 4000,則應將*ColumnSize*設置為**SQL_SS_LENGTH_UNLIMITED**以便驅動程式將使用**nvarchar(max)。**  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter 和資料表值參數  
 與其他參數類型一樣,表值參數由 SQLBind 參數綁定。  
  
 繫結資料表值參數之後，也會一併繫結其資料行。 要綁定列,請調用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以將SQL_SOPT_SS_PARAM_FOCUS設置為表值參數的表值參數的表位。 然後,為表值參數中的每個列調用 SQLBind 參數。 若要傳回到最上層參數繫結，將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0。  
  
 有關將參數對應到表值參數的描述符位元資訊,請參考[表值參數與欄值的結合與資料傳輸](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter 對增強型日期和時間功能的支援  
 日期/時間類型的參數值將轉換,如從[C 到 SQL 的轉換](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)中所述。 請注意,如果使用相應的結構 **(SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT),** 則類型**時間和****日期時間偏移**的參數必須指定*ValueType*為**SQL_C_DEFAULT**或**SQL_C_BINARY。**  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLBindParameter 支援  
 **SQLBind參數**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 進行詳細資訊](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter 函式](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
