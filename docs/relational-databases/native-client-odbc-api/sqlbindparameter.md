---
title: SQLBindParameter | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67fb8dafdabb4a9a9df60c4592f206c9106224ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115246"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBindParameter**可以消除資料轉換時用來提供資料的負擔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，導致效能大幅提升應用程式的用戶端和伺服器元件。 其他優點包括插入或更新近似的數值資料類型時，降低有效位數的損失。  
  
> [!NOTE]  
>  插入時**char**並**wchar**使用類型資料插入 image 資料行時，傳入資料的大小，而不是一種二進位格式的轉換後資料的大小。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式在任何參數陣列的單一陣列元素上碰到錯誤，驅動程式會繼續執行其餘陣列元素的陳述式。 如果應用程式已經繫結陳述式的參數狀態元素陣列，可以從陣列判斷產生錯誤的參數資料列。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式，指定繫結輸入參數時的 SQL_PARAM_INPUT。 繫結使用 OUTPUT 關鍵字定義的預存程序參數時，只會指定 SQL_PARAM_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT。  
  
 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)是與不可靠[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，如果繫結參數陣列的陣列項目會造成陳述式執行中的錯誤。 ODBC 陳述式屬性 SQL_ATTR_PARAMS_PROCESSED_PTR 會報告錯誤發生前處理的資料列數目。 接著，如果需要，此應用程式可以周遊其參數狀態陣列以探索成功執行的陳述式數目。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 字元類型的繫結參數  
 如果傳入的 SQL 資料類型是字元類型， *ColumnSize*是以字元為單位 （而不是個位元組） 的大小。 如果資料字串，以位元組為單位的長度大於 8000 *ColumnSize*應設為**SQL_SS_LENGTH_UNLIMITED**，表示為 SQL 類型的大小沒有限制。  
  
 比方說，如果 SQL 資料類型是**SQL_WVARCHAR**， *ColumnSize*不能超過 4000。 如果實際資料長度大於 4000，然後*ColumnSize*應設為**SQL_SS_LENGTH_UNLIMITED**以便**nvarchar （max)** 將驅動程式所使用。  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter 和資料表值參數  
 如同其他參數類型，資料表值參數是由 SQLBindParameter 繫結。  
  
 繫結資料表值參數之後，也會一併繫結其資料行。 若要繫結資料行，請呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以便將 SQL_SOPT_SS_PARAM_FOCUS 設定為資料表值參數的序數。 接著，呼叫 SQLBindParameter 資料表值參數中的每一個資料行。 若要傳回到最上層參數繫結，將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0。  
  
 將參數對應到資料表值參數的描述項欄位的相關資訊，請參閱[繫結和 Data Transfer of Table-Valued 參數和資料行值](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如需有關資料表值參數的詳細資訊，請參閱 < [Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter 對增強型日期和時間功能的支援  
 參數值的日期/時間類型轉換中所述[從 C 轉換成 SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)。 請注意該型別參數的**時間**並**datetimeoffset**必須要有*ValueType*指定為**SQL_C_DEFAULT**或**SQL_C_BINARY**如果及其對應的結構 (**SQL_SS_TIME2_STRUCT**並**SQL_SS_TIMESTAMPOFFSET_STRUCT**) 使用。  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLBindParameter 支援  
 **SQLBindParameter**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱 < [Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter 函式](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
