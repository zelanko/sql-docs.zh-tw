---
title: 用於表值參數的 ODBC SQL 類型 |微軟文件
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
ms.openlocfilehash: 6aae522544f4d9532dbc2d71db1b3d55ebee3da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297838"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>資料表值參數的 ODBC SQL 類型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  資料表值參數的支援是由新的 ODBC SQL 類型，也就是 SQL_SS_TABLE 所提供。  
  
## <a name="remarks"></a>備註  
 SQL_SS_TABLE 無法轉換為其他任何 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 SQL_SS_TABLE 如果在 SQLBind 參數*的 ValueType*參數中用作 C 資料類型,或者嘗試將應用程式參數描述符 (APD) 記錄中的SQL_DESC_TYPE設置為SQL_SS_TABLE,則返回SQL_ERROR,並生成使用 SQLSTATE_HY003"無效應用程式緩衝區類型"的診斷記錄。  
  
 如果 SQL_DESC_TYPE 在 IPD 記錄中設定為 SQL_SS_TABLE，而且對應的應用程式參數描述項記錄不是 SQL_C_DEFAULT，則會傳回 SQL_ERROR，並產生包含 SQLSTATE=HY003 以及「無效的應用程式緩衝區類型」的診斷記錄。 這可以通過 SQLSetDescField、SQLSetDescRec 或 SQLBind 參數的*參數類型*發生。  
  
 如果在調用 SQLGetData 時SQL_SS_TABLE *TargetType*參數,則返回SQL_ERROR,並生成使用 SQLSTATE_HY003"無效應用程式緩衝區類型"的診斷記錄。  
  
 資料表值參數資料行無法當做 SQL_SS_TABLE 類型繫結。 如果**SQLBind 參數**調用*參數設定為*SQL_SS_TABLE,則返回SQL_ERROR,並生成使用 SQLSTATE_HY004"無效 SQL 資料類型"的診斷記錄。 SQLSetDescField 和 SQLSetDescRec 也可能發生這種情況。  
  
 資料表值參數資料行值與參數和結果資料行的資料轉換選項相同。  
  
 資料表值參數在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中僅能是輸入參數。 如果嘗試透過 SQLBind 參數或 SQLSetDescField 將SQL_DESC_PARAMETER_TYPE設定為SQL_PARAM_INPUT以外的值,則會返回SQL_ERROR並將診斷記錄添加到具有 SQLSTATE_HY105 和消息"無效參數類型"的語句中。  
  
 表值參數列不能在*StrLen_or_IndPtr*中使用SQL_DEFAULT_PARAM,因為表值參數不支援每行預設值。 不過，應用程式會將資料行屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 設定為 1。 這表示資料行的所有資料列都會有預設值。 如果*StrLen_or_IndPtr*設定為SQL_DEFAULT_PARAM,SQLExecute 或 SQLExecDirect 將返回SQL_ERROR,並且診斷記錄將添加到具有 SQLSTATE_HY090 和消息"無效字串或緩衝區長度"的消息的語句中。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
