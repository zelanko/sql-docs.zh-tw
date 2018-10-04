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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6659f2abe2a167ece55aa8d6a9bbc99065f56613
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606757"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSetDescField 可用來設定資料表值參數和資料表值參數資料行的描述項欄位。 如需可用的欄位資訊，請參閱[資料表值參數描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)並[資料表值參數組成資料行的描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)。  
  
## <a name="remarks"></a>備註  
 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱 < [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 如果嘗試將 SQL_SOPT_SS_PARAM_FOCUS 設定為不是資料表值參數之參數的序數，SQLSetStmtAttr 傳回 SQL_ERROR，而且診斷記錄建立包含 SQLSTATE = HY024 和訊息 「 無效的屬性值 」。 當傳回 SQL_ERROR 時，SQL_SOPT_SS_PARAM_FOCUS 不會變更。  
  
 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原參數之描述項記錄的存取權。  
  
 如需有關資料表值參數的詳細資訊，請參閱 < [Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSetDescField 支援  
 ODBC 中已經增強了日期/時間功能。 提供新的日期/時間類型的描述項欄位的相關資訊，請參閱[參數和結果中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSetDescField 支援  
 SQLSetDescField 支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱 < [Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLSetDescField 支援  
 SQLSetDecField 可用來將 SQL_SOPT_SS_NAME_SCOPE 設定為的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 應用程式參數描述項 (APD) 中。  
  
 如需詳細資訊，請參閱 <<c0> [ 疏鬆資料行支援&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetDescField](http://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
