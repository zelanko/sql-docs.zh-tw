---
title: 表值參數的資料傳輸
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b7eecfdac3d42b7a3d8d66ffe1f8ac68652230f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304493"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>資料表值參數和資料行值的繫結與資料傳送
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  資料表值參數與其他參數一樣，必須先繫結，然後才能傳遞至伺服器。 應用程式繫結表值參數的方式與綁定其他參數的方式相同:透過使用 SQLBind 參數或等效調用 SQLSetDescField 或 SQLSetDescRec。 資料表值參數的伺服器資料類型是 SQL_SS_TABLE。 C 類型可以指定為 SQL_C_DEFAULT 或 SQL_C_BINARY。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中，只支援輸入資料表值參數。 因此，如果您嘗試將 SQL_DESC_PARAMETER_TYPE 設定為 SQL_PARAM_INPUT 以外的值，將會傳回含有 SQLSTATE = HY105 和「無效的參數類型」訊息的 SQL_ERROR。  
  
 您可以使用屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE，將預設值指派給整個資料表值參數資料行。 但是,無法使用 sqlBind*參數StrLen_or_IndPtr中*使用SQL_DEFAULT_PARAM來分配單個表值參數列值。 不能透過將SQL_DEFAULT_PARAM與 SQLBind 參數一起使用*StrLen_or_IndPtr,* 將整個表值參數設置為預設值。 如果未遵循這些規則,SQLExecute 或 SQLExecDirect 將返回SQL_ERROR。 將使用 SQLSTATE_07S01 和消息\<「參數 p>的默认参数无效使用」生成\<診斷記錄,其中 p>是查询语句中 TVP 的表位。  
  
 繫結資料表值參數之後，應用程式必須接著繫結每個資料表值參數資料行。 為此,應用程式首先調用 SQLSetStmtAttr 將SQL_SOPT_SS_PARAM_FOCUS設置為表值參數的表位。 然後,應用程式通過調用以下例程(SQLBind參數、SQLSetDescRec 和 SQLSetDescField)綁定表值參數的列。 將SQL_SOPT_SS_PARAM_FOCUS設置為 0 將恢復 SQLBind 參數、SQLSetDescRec 和 SQLSetDescField 在常規頂級參數上操作的通常效果。
 
 注意:對於具有 unixODBC 2.3.1 到 2.3.4 的 Linux 和 Mac ODBC 驅動程式,當使用SQL_CA_SS_TYPE_NAME描述符欄位透過 SQLSetDescField 設置 TVP 名稱時,unixODBC 不會根據調用的確切函數(SQLSetDescFieldA/ SQLSetDescfieldW)自動在 ANSI 和 Unicode 字串之間轉換。 必須始終使用 SQLBind 參數或 SQLSetDescFieldW 與 Unicode (UTF-16) 字串來設置 TVP 名稱。
  
 雖然不會針對資料表值參數本身傳送或接收任何實際資料，但是會針對每個構成的資料行傳送或接收資料。 由於表值參數是偽列,因此 SQLBind 參數的參數用於參考與其他資料類型不同的屬性,如下所示:  
  
|參數|非表值參數類型的相關屬性,包括欄位|資料表值參數的相關屬性|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 若為資料表值參數資料行，這必須與資料表值參數本身的設定相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 這必須是 SQL_PARAM_INPUT。|  
|*值類型*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 這必須是 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*參數類型*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 這必須是 SQL_SS_TABLE。|  
|*ColumnSize*|IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 這取決於*參數型態的值*。|SQL_DESC_ARRAY_SIZE<br /><br /> 當參數焦點設定為資料表值參數時，也可以使用 SQL_ATTR_PARAM_SET_SIZE 來設定。<br /><br /> 如果是資料表值參數，這就是資料表值參數資料行緩衝區中的資料列數目。|  
|*DecimalDigits*|IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用的。 這必須是 0。<br /><br /> 如果此參數不是 0,SQLBind 參數將返回SQL_ERROR,並且將生成診斷記錄與 SQLSTATE® HY104 和消息"無效精度或縮放」。。|  
|*參數值Ptr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 這個參數對於預存程序呼叫而言是選擇性的，如果不需要的話可以指定 NULL。 您必須針對不是程序呼叫的 SQL 陳述式指定這個參數。<br /><br /> 這個參數也會當做一個唯一值，應用程式可以在使用變動資料列繫結時使用這個值來識別這個資料表值參數。 如需詳細資訊，請參閱本主題後面的「變動資料表值參數資料列繫結」一節。<br /><br /> 當在調用 SQLBindParameter 時指定表值參數類型名稱時,必須將其指定為 Unicode 值,即使在構建為 ANSI 應用程式的應用程式中也是如此。 參數*StrLen_or_IndPtr*使用的值應為SQL_NTS,或者名稱的字串長度乘以大小(WCHAR)。|  
|*緩衝區長度*|APD 中的 SQL_DESC_OCTET_LENGTH。|資料表值參數類型名稱的長度 (以位元組為單位)。<br /><br /> 如果此類型名稱以 Null 結尾，這項設定可以是 SQL_NTS；如果不需要資料表值參數類型名稱則為 0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 若為資料表值參數，這就是資料列計數而非資料長度。|  
||||

 資料表值參數支援兩種資料傳送模式：固定資料列繫結和變動資料列繫結。  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>固定資料表值參數資料列繫結  
 對於固定資料列繫結而言，應用程式會針對所有可能的輸入資料行值配置夠大的緩衝區 (或緩衝區陣列)。 此應用程式會進行下列作業：  
  
1.  使用 SQLBind 參數、SQLSetDescRec 或 SQLSetDescField 調用綁定所有參數。  
  
    1.  將 SQL_DESC_ARRAY_SIZE 設定為可針對每個資料表值參數傳送的最大資料列數目。 這可以在 SQLBind 參數調用中完成。  
  
2.  調用 SQLSetStmtAttr 將SQL_SOPT_SS_PARAM_FOCUS設置為每個表值參數的表位。  
  
    1.  對於每個表值參數,使用 SQLBind 參數、SQLSetDescRec 或 SQLSetDescField 調用繫結表值參數列。  
  
    2.  對於每個具有預設值的表值參數列,調用 SQLSetDescField 將SQL_CA_SS_COL_HAS_DEFAULT_VALUE設置為 1。  
  
3.  調用 SQLSetStmtAttr 將SQL_SOPT_SS_PARAM_FOCUS設置為 0。 在調用 SQLExecute 或 SQLExecDirect 之前,必須完成此操作。 否則，系統將傳回 SQL_ERROR，並產生包含 SQLSTATE=HY024 和「屬性值 SQL_SOPT_SS_PARAM_FOCUS 無效 (在執行時間必須為零)」訊息的診斷記錄。  
  
4.  將*StrLen_or_IndPtr*或SQL_DESC_OCTET_LENGTH_PTR集,以SQL_DEFAULT_PARAM沒有行的表值參數,或者將 SQLExecute 或 SQLExecDirect 的下一次調用時傳輸的行數(如果表值參數具有行)。 *StrLen_or_IndPtr*或SQL_DESC_OCTET_LENGTH_PTR無法設置為表值參數的SQL_NULL_DATA,因為表值參數不是空的(儘管表值參數組成列可能是空的)。 如果將其設置為無效值,SQLExecute 或 SQLExecDirect 將返回SQL_ERROR,並且使用 SQLSTATE_HY090\<和消息"參數 p>的无效字符串或缓冲区长度"生成診斷記錄,其中 p 是參數編號。  
  
5.  呼叫 SQLExecute 或 SQLExecDirect。  
  
 如果*StrLen_or_IndPtr*設定為SQL_LEN_DATA_AT_EXEC(*長度*)或SQL_DATA_AT_EXEC,則可以分段傳遞輸入表值參數列值。 這與使用參數陣列時分段傳遞值一樣。 與執行時所有資料參數一樣,SQLParamData 不指示驅動程式請求數據的陣列的哪一行;應用程式必須處理好這一點。 應用程式無法針對驅動程式要求值的順序提出任何假設。  
  
## <a name="variable-table-valued-parameter-row-binding"></a>變動資料表值參數資料列繫結  
 對於變動資料列繫結而言，資料列會在執行階段按照批次傳送，而且應用程式會視需要將資料列傳遞至驅動程式。 這與個別參數值的資料執行中一樣。 應用程式會針對變動資料列繫結，執行下列作業：  
  
1.  依照上一節「固定資料表值參數資料列繫結」的步驟 1 到 3 所述，繫結參數和資料表值參數資料行。  
  
2.  為在執行時傳遞給SQL_DATA_AT_EXEC的任何表值參數設置*StrLen_or_IndPtr*或SQL_DESC_OCTET_LENGTH_PTR。 如果沒有設定任何項目，就會依照上一節所述的方式處理此參數。  
  
3.  呼叫 SQLExecute 或 SQLExecDirect。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 參數要當做資料執行中參數處理，這就會傳回 SQL_NEED_DATA。 在此情況下，應用程式會進行下列作業：  
  
    -   調用 SQLParamData。 這將返回執行時數據參數的*參數ValuePtr*值和SQL_NEED_DATA返回代碼。 將所有參數數據傳遞給驅動程式后,SQLParamData 將返回SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或SQL_ERROR。 對於執行時的資料參數,*參數 ValuePtr(* 與描述符位SQL_DESC_DATA_PTR相同)可視為唯一識別需要值的參數的權杖。 這個 "Token" 會在繫結階段從應用程式傳遞至驅動程式，然後在執行階段傳回應用程式。  
  
4.  要發送空表值參數的表值參數行資料,如果表值參數沒有行,則應用程式將 SQLPutData 調用 *,StrLen_or_Ind*設置為SQL_DEFAULT_PARAM。  
  
     應用程式會針對非 NULL TVP：  
  
    -   將所有表值參數列*的Str_Len_or_Ind*設置為適當的值,併為不為執行時的數據值參數列填充數據緩衝區。 您可以利用一般參數分段傳遞至驅動程式的相同方式來運用資料表值參數資料行的資料執行中。  
  
    -   呼叫*SQLPutData,Str_Len_or_Ind*設定為要發送到伺服器的行數。 超出 0 到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 之範圍以外的任何值都是錯誤，而且將傳回 SQLSTATE HY090 以及「無效的字串或緩衝區長度」訊息。 0 表示已經傳送所有資料列，而且資料表值參數沒有其他資料 (如此清單中第二個項目符號項目所述)。 只有當驅動程式第一次要求資料表值參數的資料時，才能使用 SQL_DEFAULT_PARAM (如此清單中第一個項目符號項目所述)。  
  
5.  發送所有行后,調用 sqlPutData 的表值參數的值*Str_Len_or_Ind為*0,然後繼續執行上面的步驟 3a。  
  
6.  再次調用 SQLParamData。 如果表值參數列中有任何資料執行參數,則這些參數將由 SQLParamData 返回的值*ValuePtrPtr*標識。 當所有列值都可用時,SQLParamData 將再次返回表值參數的*參數ValuePtr*值,應用程式將再次啟動。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
