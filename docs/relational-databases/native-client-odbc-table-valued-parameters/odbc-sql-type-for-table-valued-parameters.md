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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9eb67883cd580aecee8b4e41eae67c3e2dfc4856
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129206"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>資料表值參數的 ODBC SQL 類型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  資料表值參數的支援是由新的 ODBC SQL 類型，也就是 SQL_SS_TABLE 所提供。  
  
## <a name="remarks"></a>備註  
 SQL_SS_TABLE 無法轉換為其他任何 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 如果 SQL_SS_TABLE 做為中的 C 資料類型*ValueType*有人 SQLBindParameter 或嘗試的參數為 SQL_SS_TABLE 的應用程式參數描述項 (APD) 記錄中的 SQL_DESC_TYPE 設定時，會傳回 SQL_ERROR，診斷記錄就會產生含有 SQLSTATE sqlstate=hy003 以及 「 無效的應用程式緩衝區類型 」。  
  
 如果 SQL_DESC_TYPE 在 IPD 記錄中設定為 SQL_SS_TABLE，而且對應的應用程式參數描述項記錄不是 SQL_C_DEFAULT，則會傳回 SQL_ERROR，並產生包含 SQLSTATE=HY003 以及「無效的應用程式緩衝區類型」的診斷記錄。 這可能會發生*ParameterType* SQLSetDescField、 SQLSetDescRec 或 SQLBindParameter。  
  
 如果*TargetType*呼叫 SQLGetData 時，參數為 SQL_SS_TABLE，則會傳回 SQL_ERROR，並將診斷記錄就會產生含有 SQLSTATE sqlstate=hy003 以及 「 無效的應用程式緩衝區類型 」。  
  
 資料表值參數資料行無法當做 SQL_SS_TABLE 類型繫結。 如果**SQLBindParameter**呼叫*ParameterType*設定為 SQL_SS_TABLE，則會傳回 SQL_ERROR，並診斷記錄就會產生含有 SQLSTATE sqlstate=hy004 以及 「 無效的 SQL 資料類型 」。 這也可以利用 SQLSetDescField 和 SQLSetDescRec。  
  
 資料表值參數資料行值與參數和結果資料行的資料轉換選項相同。  
  
 資料表值參數在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中僅能是輸入參數。 如果嘗試將 SQL_DESC_PARAMETER_TYPE 設定為透過 SQLBindParameter 或 SQLSetDescField SQL_PARAM_INPUT 以外的值，則會傳回 SQL_ERROR，而且診斷記錄加入陳述式 = 包含 sqlstate=hy105 和訊息 「 無效的參數型別 」。  
  
 資料表值參數資料行中無法使用 SQL_DEFAULT_PARAM *StrLen_or_IndPtr*，因為資料表值參數不支援每個資料列的預設值。 不過，應用程式會將資料行屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 設定為 1。 這表示資料行的所有資料列都會有預設值。 如果*StrLen_or_IndPtr*會設定為 SQL_DEFAULT_PARAM，SQLExecute 或 SQLExecDirect 會傳回 SQL_ERROR，並將診斷記錄將會加入至陳述式包含 sqlstate=hy090 和 「 無效的字串或緩衝區長度 」 的訊息。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
