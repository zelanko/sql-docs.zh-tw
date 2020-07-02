---
title: 資料表值參數的 ODBC SQL 類型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 96e74ebafcf6d80ba3db5a609209dcb79339d71e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783188"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>資料表值參數的 ODBC SQL 類型
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  資料表值參數的支援是由新的 ODBC SQL 類型，也就是 SQL_SS_TABLE 所提供。  
  
## <a name="remarks"></a>備註  
 SQL_SS_TABLE 無法轉換為其他任何 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 如果在 SQLBindParameter 的*ValueType*參數中使用 SQL_SS_TABLE 做為 C 資料類型，或嘗試將應用程式參數描述項（APD）記錄中的 SQL_DESC_TYPE 設定為 SQL_SS_TABLE，則會傳回 SQL_ERROR，並使用 SQLSTATE = hy003 以及（「不正確應用程式緩衝區類型」）來產生診斷記錄。  
  
 如果 SQL_DESC_TYPE 在 IPD 記錄中設定為 SQL_SS_TABLE，而且對應的應用程式參數描述項記錄不是 SQL_C_DEFAULT，則會傳回 SQL_ERROR，並產生包含 SQLSTATE=HY003 以及「無效的應用程式緩衝區類型」的診斷記錄。 SQLSetDescField、SQLSetDescRec 或 SQLBindParameter 的*ParameterType*可能會發生這種情況。  
  
 如果在呼叫 SQLGetData 時 SQL_SS_TABLE *TargetType*參數，SQL_ERROR 會傳回，而且會產生含有 SQLSTATE = hy003 以及，「不正確應用程式緩衝區類型」的診斷記錄。  
  
 資料表值參數資料行無法當做 SQL_SS_TABLE 類型繫結。 如果呼叫**SQLBindParameter**時， *ParameterType*設定為 SQL_SS_TABLE，則會傳回 SQL_ERROR，並使用 SQLSTATE = HY004 「不正確 SQL 資料類型」來產生診斷記錄。 SQLSetDescField 和 SQLSetDescRec 也會發生這種情況。  
  
 資料表值參數資料行值與參數和結果資料行的資料轉換選項相同。  
  
 資料表值參數在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中僅能是輸入參數。 如果嘗試將 SQL_DESC_PARAMETER_TYPE 設定為 SQL_PARAM_INPUT via SQLBindParameter 或 SQLSetDescField 以外的值，則會傳回 SQL_ERROR，並將診斷記錄新增至具有 SQLSTATE = HY105 和訊息「不正確參數類型」的語句中。  
  
 資料表值參數資料行無法在*StrLen_or_IndPtr*中使用 SQL_DEFAULT_PARAM，因為資料表值參數不支援每個資料列的預設值。 不過，應用程式會將資料行屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 設定為 1。 這表示資料行的所有資料列都會有預設值。 如果*StrLen_or_IndPtr*設定為 SQL_DEFAULT_PARAM，SQLExecute 或 SQLExecDirect 會傳回 SQL_ERROR，而診斷記錄將會加入具有 SQLSTATE = HY090 和訊息「不正確字串或緩衝區長度」的語句中。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
