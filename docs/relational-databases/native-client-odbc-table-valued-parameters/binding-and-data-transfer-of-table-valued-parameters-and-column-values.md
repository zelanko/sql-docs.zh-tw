---
title: 繫結和資料傳輸的資料表值參數和資料行值 |Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f8b291344939bcbafa7f91080837d2302efb1d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62738554"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>資料表值參數和資料行值的繫結與資料傳送
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  資料表值參數與其他參數一樣，必須先繫結，然後才能傳遞至伺服器。 應用程式繫結資料表值參數與其他參數的方式相同： 使用 SQLBindParameter 或 SQLSetDescField 或 SQLSetDescRec 同等的呼叫。 資料表值參數的伺服器資料類型是 SQL_SS_TABLE。 C 類型可以指定為 SQL_C_DEFAULT 或 SQL_C_BINARY。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中，只支援輸入資料表值參數。 因此，如果您嘗試將 SQL_DESC_PARAMETER_TYPE 設定為 SQL_PARAM_INPUT 以外的值，將會傳回含有 SQLSTATE = HY105 和「無效的參數類型」訊息的 SQL_ERROR。  
  
 您可以使用屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE，將預設值指派給整個資料表值參數資料行。 個別的資料表值參數資料行，不過，無法將值指派預設值中使用 SQL_DEFAULT_PARAM *StrLen_or_IndPtr* SQLBindParameter 使用。 整體的資料表值參數不能設定為預設值中使用 SQL_DEFAULT_PARAM *StrLen_or_IndPtr* SQLBindParameter 使用。 如果未遵循這些規則，SQLExecute 或 SQLExecDirect 就會傳回 SQL_ERROR。 診斷記錄會產生含有 SQLSTATE = 07S01 和訊息 」 的預設參數位置參數用法無效\<p >"，其中\<p > 是查詢陳述式中 TVP 的序數。  
  
 繫結資料表值參數之後，應用程式必須接著繫結每個資料表值參數資料行。 若要這樣做，應用程式會先呼叫 SQLSetStmtAttr 以便將 SQL_SOPT_SS_PARAM_FOCUS 設定為資料表值參數的序數。 然後應用程式繫結資料表值參數的資料行，藉由呼叫下列常式：SQLBindParameter、 SQLSetDescRec 和 SQLSetDescField。 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原 SQLBindParameter、 SQLSetDescRec 和 SQLSetDescField 的一般作用中規則的最上層參數運作。
 
 注意： unixODBC 2.3.1 至 2.3.4，設定與 SQL_CA_SS_TYPE_NAME 描述項欄位透過 SQLSetDescField TVP 名稱時使用的 Linux 和 Mac 的 ODBC 驅動程式，如 unixODBC 不會自動轉換 ANSI 和 Unicode 間取決於確切的字串呼叫函式 (SQLSetDescFieldA / SQLSetDescFieldW)。 必須一律使用 SQLBindParameter 或 SQLSetDescFieldW 以 Unicode (utf-16) 字串 TVP 名稱設定。
  
 雖然不會針對資料表值參數本身傳送或接收任何實際資料，但是會針對每個構成的資料行傳送或接收資料。 因為資料表值參數是虛擬資料行，用以 SQLBindParameter 的參數，如下所示不同的屬性，而其他資料類型，請參閱：  
  
|參數|對於非資料表值參數類型，包括資料行相關聯的屬性|資料表值參數的相關屬性|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 若為資料表值參數資料行，這必須與資料表值參數本身的設定相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 這必須是 SQL_PARAM_INPUT。|  
|*ValueType*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 這必須是 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*ParameterType*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 這必須是 SQL_SS_TABLE。|  
|*ColumnSize*|IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 這取決於 windows 7 *ParameterType*。|SQL_DESC_ARRAY_SIZE<br /><br /> 當參數焦點設定為資料表值參數時，也可以使用 SQL_ATTR_PARAM_SET_SIZE 來設定。<br /><br /> 如果是資料表值參數，這就是資料表值參數資料行緩衝區中的資料列數目。|  
|*DecimalDigits*|IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用的。 這必須是 0。<br /><br /> 如果這個參數是不 0、 SQLBindParameter 會傳回 SQL_ERROR，並將診斷記錄會產生含有 SQLSTATE = HY104 和訊息 「 無效的有效位數或小數位數 」。|  
|*ParameterValuePtr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 這個參數對於預存程序呼叫而言是選擇性的，如果不需要的話可以指定 NULL。 您必須針對不是程序呼叫的 SQL 陳述式指定這個參數。<br /><br /> 這個參數也會當做一個唯一值，應用程式可以在使用變動資料列繫結時使用這個值來識別這個資料表值參數。 如需詳細資訊，請參閱本主題後面的「變動資料表值參數資料列繫結」一節。<br /><br /> SQLBindParameter 的呼叫上指定的資料表值參數類型名稱時，它必須指定為 Unicode 值，即使在建置為 ANSI 應用程式的應用程式。 使用參數的值*StrLen_or_IndPtr*應該是 SQL_NTS 或是字串長度乘以 sizeof （wchar） 的名稱。|  
|*BufferLength*|APD 中的 SQL_DESC_OCTET_LENGTH。|資料表值參數類型名稱的長度 (以位元組為單位)。<br /><br /> 如果此類型名稱以 Null 結尾，這項設定可以是 SQL_NTS；如果不需要資料表值參數類型名稱則為 0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 若為資料表值參數，這就是資料列計數而非資料長度。|  
  
 資料表值參數支援兩種資料傳送模式：固定資料列繫結和變動資料列繫結。  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>固定資料表值參數資料列繫結  
 對於固定資料列繫結而言，應用程式會針對所有可能的輸入資料行值配置夠大的緩衝區 (或緩衝區陣列)。 此應用程式會進行下列作業：  
  
1.  使用 SQLBindParameter、 SQLSetDescRec 或 SQLSetDescField 呼叫繫結所有參數。  
  
    1.  將 SQL_DESC_ARRAY_SIZE 設定為可針對每個資料表值參數傳送的最大資料列數目。 這可以在 SQLBindParameter 呼叫中。  
  
2.  呼叫 SQLSetStmtAttr 將 SQL_SOPT_SS_PARAM_FOCUS 設定為每個資料表值參數的序數。  
  
    1.  每個資料表值參數，請使用 SQLBindParameter、 SQLSetDescRec 或 SQLSetDescField 呼叫繫結資料表值參數資料行。  
  
    2.  每個資料表值參數資料行，都有預設值，會呼叫 SQLSetDescField 以便將 sql_ca_ss_col_has_default_value 設定為 1。  
  
3.  呼叫 SQLSetStmtAttr 以便將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0。 SQLExecute 之前必須完成，或稱為 SQLExecDirect。 否則，系統將傳回 SQL_ERROR，並產生包含 SQLSTATE=HY024 和「屬性值 SQL_SOPT_SS_PARAM_FOCUS 無效 (在執行時間必須為零)」訊息的診斷記錄。  
  
4.  設定組*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 為 SQL_DEFAULT_PARAM，沒有資料列或資料列數目的資料表值參數傳送的下一個呼叫 SQLExecute 或 SQLExecDirect，如果資料表值參數的資料列。 *StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 無法設定為 SQL_NULL_DATA 資料表值參數為資料表值參數不可以是 null （不過資料表值參數組成資料行可為 null）。 如果這設定為無效的值，SQLExecute 或 SQLExecDirect 就會傳回 SQL_ERROR，而且診斷記錄就會產生含有 SQLSTATE = HY090 以及訊息 「 無效的字串或緩衝區長度參數\<p >"，其中 p 是參數編號。  
  
5.  SQLExecute 或 SQLExecDirect 呼叫。  
  
 輸入可以分段傳遞資料表值參數資料行值，是否*StrLen_or_IndPtr*設定為 SQL_LEN_DATA_AT_EXEC (*長度*) 或 SQL_DATA_AT_EXEC，資料行。 這與使用參數陣列時分段傳遞值一樣。 因為所有資料在執行中參數，使用 SQLParamData 不會指出哪一個資料列陣列的驅動程式會要求資料;應用程式必須解決此問題。 應用程式無法針對驅動程式要求值的順序提出任何假設。  
  
## <a name="variable-table-valued-parameter-row-binding"></a>變動資料表值參數資料列繫結  
 對於變動資料列繫結而言，資料列會在執行階段按照批次傳送，而且應用程式會視需要將資料列傳遞至驅動程式。 這與個別參數值的資料執行中一樣。 應用程式會針對變動資料列繫結，執行下列作業：  
  
1.  依照上一節「固定資料表值參數資料列繫結」的步驟 1 到 3 所述，繫結參數和資料表值參數資料行。  
  
2.  設定組*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 為 SQL_DATA_AT_EXEC，在執行階段傳遞任何資料表值參數。 如果沒有設定任何項目，就會依照上一節所述的方式處理此參數。  
  
3.  SQLExecute 或 SQLExecDirect 呼叫。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 參數要當做資料執行中參數處理，這就會傳回 SQL_NEED_DATA。 在此情況下，應用程式會進行下列作業：  
  
    -   呼叫 SQLParamData。 這會傳回*ParameterValuePtr*資料在執行中參數和 SQL_NEED_DATA 的傳回碼值。 當所有參數資料已都傳遞至驅動程式時，SQLParamData 會傳回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 資料在執行中參數，如*ParameterValuePtr*，相當於與描述項欄位 SQL_DESC_DATA_PTR、 可以被視為語彙基元來唯一識別值是必要的參數。 這個 "Token" 會在繫結階段從應用程式傳遞至驅動程式，然後在執行階段傳回應用程式。  
  
4.  若要傳送 null 資料表值參數時，資料表值參數資料列的資料，如果資料表值參數不有任何資料列，應用程式會呼叫與 SQLPutData *Strlen_or_ind&lt*設定為 SQL_DEFAULT_PARAM。  
  
     應用程式會針對非 NULL TVP：  
  
    -   設定組*Str_Len_or_Ind*為適當的值的所有資料表值參數資料行，並填入資料表值參數資料行不是要成為資料在執行中參數的資料緩衝區。 您可以利用一般參數分段傳遞至驅動程式的相同方式來運用資料表值參數資料行的資料執行中。  
  
    -   呼叫以 SQLPutData *Str_Len_or_Ind*設定為資料列數目，以傳送到伺服器。 超出 0 到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 之範圍以外的任何值都是錯誤，而且將傳回 SQLSTATE HY090 以及「無效的字串或緩衝區長度」訊息。 0 表示已經傳送所有資料列，而且資料表值參數沒有其他資料 (如此清單中第二個項目符號項目所述)。 只有當驅動程式第一次要求資料表值參數的資料時，才能使用 SQL_DEFAULT_PARAM (如此清單中第一個項目符號項目所述)。  
  
5.  傳送所有資料列後，會使用資料表值參數呼叫 SQLPutData *Str_Len_or_Ind*值為 0，然後繼續進行上面的步驟 3a。  
  
6.  會再次呼叫 SQLParamData。 如果有任何資料表值參數資料行之間的資料在執行參數，將會識別這些值所*ValuePtrPtr* SQLParamData 所傳回。 所有資料行值可用時，會再次傳回 SQLParamData *ParameterValuePtr*資料表值參數，和應用程式的值重新開始。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
