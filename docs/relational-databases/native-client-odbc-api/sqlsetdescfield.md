---
title: SQLSetDescField |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a37821dff5176dfcb42cfd0a9f6424dfcc3f1938
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785701"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField 可以用來設定資料表值參數和資料表值參數資料行的描述項欄位。 如需可用欄位的詳細資訊，請參閱資料表值參數組成資料[行的](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)[資料表值參數描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)和描述項欄位。  
  
## <a name="remarks"></a>Remarks  
 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 如需 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 如果嘗試將 SQL_SOPT_SS_PARAM_FOCUS 設定為不是資料表值參數之參數的序數，則 SQLSetStmtAttr 會傳回 SQL_ERROR，而且會使用 SQLSTATE = HY024 和訊息「不正確屬性值」來建立診斷記錄。 當傳回 SQL_ERROR 時，SQL_SOPT_SS_PARAM_FOCUS 不會變更。  
  
 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原參數之描述項記錄的存取權。  
  
 如需資料表值參數的詳細資訊，請參閱[資料表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSetDescField 支援  
 ODBC 中已經增強了日期/時間功能。 如需針對新日期/時間類型提供之描述項欄位的詳細資訊，請參閱[參數和結果中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱[日期和&#40;時間&#41;改善 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSetDescField 支援  
 SQLSetDescField 支援大型 CLR 使用者定義型別（Udt）。 如需詳細資訊，請參閱[大型 CLR 使用者定義&#40;類型&#41;ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLSetDescField 支援  
 SQLSetDecField 可以用來將應用程式參數描述項（APD）中的 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 的值。  
  
 如需詳細資訊，請參閱[Sparse &#40;資料&#41;行支援 ODBC](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
