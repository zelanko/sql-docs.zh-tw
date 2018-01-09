---
title: "SQLSetDescField |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17f8487f13b439471501ea5c3777893d19aa623c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSetDescField 可以用來設定資料表值參數和資料表值參數資料行的描述項欄位。 如需可用的欄位資訊，請參閱[資料表值參數描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)和[資料表值參數組成資料行的描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)。  
  
## <a name="remarks"></a>備註  
 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 如果嘗試將 SQL_SOPT_SS_PARAM_FOCUS 設定為不是資料表值參數之參數的序數，SQLSetStmtAttr 傳回 SQL_ERROR，並將診斷記錄會建立包含 SQLSTATE = HY024 及 「 屬性值無效 」 的訊息。 當傳回 SQL_ERROR 時，SQL_SOPT_SS_PARAM_FOCUS 不會變更。  
  
 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原參數之描述項記錄的存取權。  
  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSetDescField 支援  
 ODBC 中已經增強了日期/時間功能。 提供新的日期/時間類型的描述項欄位的相關資訊，請參閱[and Result Metadata<](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSetDescField 支援  
 SQLSetDescField 支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLSetDescField 支援  
 SQLSetDecField 可以用來將 SQL_SOPT_SS_NAME_SCOPE 設定為值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 應用程式參數描述項 (APD) 中。  
  
 如需詳細資訊，請參閱[疏鬆資料行支援 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>請參閱  
 [SQLSetDescField](http://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
