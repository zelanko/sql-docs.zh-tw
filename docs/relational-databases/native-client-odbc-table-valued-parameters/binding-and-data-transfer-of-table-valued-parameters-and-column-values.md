---
title: Table-Valued 參數的資料傳輸
description: 描述 Table-Valued 參數的資料傳輸
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: native-client
ms.topic: reference
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 07/01/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 19a7f22cd26ea4988364d51ff70300cdbf42d365
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97436100"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>資料表值參數和資料行值的繫結與資料傳送

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

資料表值參數 (TVP) （如同其他參數）必須先系結，才能傳遞至伺服器。 應用程式系結資料表值參數的方式，與系結其他參數的方式相同：使用 SQLBindParameter 或對 SQLSetDescField 或 SQLSetDescRec 的對等呼叫。 資料表值參數的伺服器資料類型是 SQL_SS_TABLE。 C 類型可以指定為 SQL_C_DEFAULT 或 SQL_C_BINARY。  

在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中，只支援輸入資料表值參數。 因此，嘗試將 SQL_DESC_PARAMETER_TYPE 設定為 SQL_PARAM_INPUT 以外的值時，會傳回具有 SQLSTATE = HY105 的 SQL_ERROR 和「不正確參數類型」訊息。  

您可以使用屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE，將預設值指派給整個資料表值參數資料行。 不過，個別的資料表值參數資料行值不能藉由使用 *StrLen_or_IndPtr* with SQLBindParameter 中的 SQL_DEFAULT_PARAM 來指派預設值。 使用 *StrLen_or_IndPtr* with SQLBindParameter 中的 SQL_DEFAULT_PARAM，無法將整個資料表值參數設定為預設值。 如果未遵循這些規則，SQLExecute 或 SQLExecDirect 會傳回 SQL_ERROR。 使用 SQLSTATE = 07S01 和「參數的預設參數用法無效」訊息產生診斷記錄 \<p> ，其中 \<p> 是查詢語句中 TVP 的序數。  

> [!Note]
> 資料表值參數沒有可設定的預設值，因為 SQL_DEFAULT_PARAM 不會指出任何資料列。 因此，如果沒有任何資料列，就不會有要系結的資料行。

繫結資料表值參數之後，應用程式必須接著繫結每個資料表值參數資料行。 若要這樣做，應用程式會先呼叫 SQLSetStmtAttr，將 SQL_SOPT_SS_PARAM_FOCUS 設定為數據表值參數的序數。 應用程式會藉由呼叫下列常式來系結資料表值參數的資料行： SQLBindParameter、SQLSetDescRec 和 SQLSetDescField。 將 SQL_SOPT_SS_PARAM_FOCUS 設定為0會還原一般最上層參數操作的 SQLBindParameter、SQLSetDescRec 和 SQLSetDescField 一般效果。

> [!Note]
> 針對具有 unixODBC 2.3.1 至2.3.4 的 Linux 和 Mac ODBC 驅動程式，使用 SQL_CA_SS_TYPE_NAME 描述項欄位透過 SQLSetDescField 設定 TVP 名稱時，根據稱為 (UnixODBC/SQLSetDescFieldA) 的確切函數，SQLSetDescFieldW 不會自動在 ANSI 和 Unicode 字串之間轉換。 您必須一律使用 SQLBindParameter 或 SQLSetDescFieldW 搭配 Unicode (UTF-16) 字串來設定 TVP 名稱。

雖然不會針對資料表值參數本身傳送或接收任何實際資料，但是會針對每個構成的資料行傳送或接收資料。 因為資料表值參數是虛擬資料行，所以 SQLBindParameter 的參數會參考與其他資料類型不同的屬性，如下所示：  

| 參數 | 非資料表值參數類型的相關屬性，包括資料行 | 資料表值參數的相關屬性 |
|-----------|---------------------------------------------------------------------------|-----------------------------------------------|
|*InputOutputType*|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 若為資料表值參數資料行，這必須與資料表值參數本身的設定相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 這必須是 SQL_PARAM_INPUT。|  
|*ValueType*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 這必須是 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*ParameterType*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 這必須是 SQL_SS_TABLE。|  
|*ColumnSize*|IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 這取決於 *ParameterType* 的值。|SQL_DESC_ARRAY_SIZE<br /><br /> 當參數焦點設定為資料表值參數時，也可以使用 SQL_ATTR_PARAM_SET_SIZE 來設定。<br /><br /> 如果是資料表值參數，這就是資料表值參數資料行緩衝區中的資料列數目。|  
|*DecimalDigits*|IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用的。 這必須是 0。<br /><br /> 如果這個參數不是0，SQLBindParameter 會傳回 SQL_ERROR，並且會產生具有 SQLSTATE = HY104 和訊息「不正確有效位數或小數位數」的診斷記錄。|  
|*ParameterValuePtr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 這對預存程序呼叫而言是選擇性的，如果不需要，也可以指定 Null。 它必須針對不是程序呼叫的 SQL 語句來指定。<br /><br /> 這個參數也會當做一個唯一值，應用程式可以在使用變動資料列繫結時使用這個值來識別這個資料表值參數。 如需詳細資訊，請參閱本主題後面的「變動資料表值參數資料列繫結」一節。<br /><br /> 在 SQLBindParameter 的呼叫上指定資料表值參數類型名稱時，必須將其指定為 Unicode 值，即使是在以 ANSI 應用程式形式建立的應用程式中也一樣。 用於參數 *StrLen_or_IndPtr* 的值應該是 SQL_NTS，或名稱的字串長度乘以 (WCHAR) 的大小。|  
|*BufferLength*|APD 中的 SQL_DESC_OCTET_LENGTH。|資料表值參數類型名稱的長度 (以位元組為單位)。<br /><br /> 如果類型名稱是以 null 結束，則可以 SQL_NTS 此值，如果不需要資料表值參數類型名稱，則為0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 若為資料表值參數，這就是資料列計數而非資料長度。|  
||||

資料表值參數支援兩種資料傳送模式：固定資料列繫結和變動資料列繫結。  

## <a name="fixed-table-valued-parameter-row-binding"></a>固定資料表值參數資料列繫結

對於固定資料列繫結而言，應用程式會針對所有可能的輸入資料行值配置夠大的緩衝區 (或緩衝區陣列)。 此應用程式會進行下列作業：  

1. 使用 SQLBindParameter、SQLSetDescRec 或 SQLSetDescField 呼叫來系結所有參數。  

    1. 將 SQL_DESC_ARRAY_SIZE 設定為可針對每個資料表值參數傳送的最大資料列數目。 這可以在 SQLBindParameter 呼叫中完成。  

2. 呼叫 SQLSetStmtAttr，將 SQL_SOPT_SS_PARAM_FOCUS 設定為每個資料表值參數的序數。  

    1. 針對每個資料表值參數，使用 SQLBindParameter、SQLSetDescRec 或 SQLSetDescField 呼叫來系結資料表值參數資料行。  

    2. 針對要擁有預設值的每個資料表值參數資料行，呼叫 SQLSetDescField 以將 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 設定為1。  

3. 呼叫 SQLSetStmtAttr 將 SQL_SOPT_SS_PARAM_FOCUS 設定為0。 這必須在呼叫 SQLExecute 或 SQLExecDirect 之前完成。 否則，會傳回 SQL_ERROR，並且會產生具有 SQLSTATE = HY024 的診斷記錄，而在執行時，SQL_SOPT_SS_PARAM_FOCUS (的屬性值必須為零) 」。  

4. 將 *StrLen_or_IndPtr* 或 SQL_DESC_OCTET_LENGTH_PTR 設定為不含資料列的資料表值參數 SQL_DEFAULT_PARAM，或設定在下一次呼叫 SQLExecute 或 SQLExecDirect 時要傳送的資料列數目（如果資料表值參數具有資料列）。 您無法將資料表值參數的 *StrLen_or_IndPtr* 或 SQL_DESC_OCTET_LENGTH_PTR 設定為 SQL_Null_DATA， (因為資料表值參數組成資料行可以是可為 null 的) 。 如果這個值設為不正確值，SQLExecute 或 SQLExecDirect 會傳回 SQL_ERROR，並且會產生包含 SQLSTATE = HY090 和「參數的字串或緩衝區長度無效」訊息的診斷記錄， \<p> 其中 p 是參數編號。

5. 呼叫 SQLExecute 或 SQLExecDirect。

    如果 *StrLen_or_IndPtr* 設定為 SQL_LEN_DATA_AT_EXEC 資料行 (*長度*) 或 SQL_DATA_AT_EXEC，則可以將輸入資料表值參數資料行值以片段傳遞。 這與使用參數陣列時分段傳遞值一樣。 如同所有資料執行中參數，SQLParamData 並不會指出驅動程式要求資料的陣列資料列;應用程式必須負責處理此情況。 應用程式無法對驅動程式要求值的順序做出任何假設。  

## <a name="variable-table-valued-parameter-row-binding"></a>變動資料表值參數資料列繫結  

若為變數資料列系結，資料列會在執行時間以批次方式傳送，而應用程式會視需要將資料列傳遞至驅動程式。 這與個別參數值的資料執行中一樣。 應用程式會針對變動資料列繫結，執行下列作業：  

1. 系結參數和資料表值參數資料行（如前一節的步驟1到3「固定 Table-Valued 參數資料列系結」所述）。  

2. 針對要在執行時間傳遞至 SQL_DATA_AT_EXEC 的任何資料表值參數，設定 *StrLen_or_IndPtr* 或 SQL_DESC_OCTET_LENGTH_PTR。 如果都未設定，則會依照上一節所述的方式來處理參數。  

3. 呼叫 SQLExecute 或 SQLExecDirect。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 參數要處理為數據執行中參數，則會傳回 SQL_NEED_DATA。 在此情況下，應用程式會進行下列作業：  

    - 呼叫 SQLParamData。 這會傳回資料執行中參數的 *ParameterValuePtr* 值，以及 SQL_NEED_DATA 的傳回碼。 當所有參數資料都傳遞至驅動程式時，SQLParamData 會傳回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 若為數據執行中參數， *ParameterValuePtr*（與描述項欄位相同 SQL_DESC_DATA_PTR）可以視為標記，以識別唯一需要值的參數。 這個 "Token" 會在繫結階段從應用程式傳遞至驅動程式，然後在執行階段傳回應用程式。  
  
4. 若要傳送 null 資料表值參數的資料表值參數資料列資料，當資料表值參數沒有任何資料列時，應用程式會呼叫 SQLPutData，並將 *StrLen_or_Ind* 設定為 SQL_DEFAULT_PARAM。  

    應用程式會針對非 NULL TVP：

    - 將所有資料表值參數資料行的 *Str_Len_or_Ind* 設定為適當的值，並針對不是資料執行中參數的資料表值參數資料行填入資料緩衝區。 您可以利用一般參數分段傳遞至驅動程式的相同方式來運用資料表值參數資料行的資料執行中。  

    - 呼叫 SQLPutData， *Str_Len_or_Ind* 設定為要傳送至伺服器的資料列數目。 範圍0到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 以外的任何值都是錯誤，而且會傳回 SQLSTATE HY090，其訊息為「不正確字串或緩衝區長度」。 0表示已傳送所有資料列，而且資料表值參數沒有其他資料 (如這份清單中的第二個專案符號專案所述) 。 只有當驅動程式第一次要求資料表值參數的資料時，才能使用 SQL_DEFAULT_PARAM (如此清單中第一個項目符號項目所述)。  

5. 當所有資料列都已傳送時，會針對 *Str_Len_or_Ind* 值為0的資料表值參數呼叫 SQLPutData，然後繼續進行上述的步驟3a。  

6. 再次呼叫 SQLParamData。 如果資料表值參數資料行之間有任何資料執行中參數，這些參數會由 SQLParamData 所傳回的值 *ValuePtrPtr* 來識別。 當所有資料行值都可供使用時，SQLParamData 會傳回資料表值參數的 *ParameterValuePtr* 值，而應用程式會重新開始。  

## <a name="next-steps"></a>後續步驟

[資料表值參數 ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)