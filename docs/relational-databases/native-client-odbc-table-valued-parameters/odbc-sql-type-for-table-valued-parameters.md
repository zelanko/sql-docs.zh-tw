---
title: "資料表值參數的 ODBC SQL 類型 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624e3886e5ae82b63fe163b60f6a118540abe523
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>資料表值參數的 ODBC SQL 類型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  資料表值參數的支援是由新的 ODBC SQL 類型，也就是 SQL_SS_TABLE 所提供。  
  
## <a name="remarks"></a>備註  
 SQL_SS_TABLE 無法轉換為其他任何 ODBC 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 如果 SQL_SS_TABLE 會使用中的 C 資料類型為*ValueType* SQLBindParameter 或嘗試參數對 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 的應用程式參數描述項 (APD) 記錄中，會傳回 SQL_ERROR，並診斷記錄產生包含 SQLSTATE = HY003 以及 「 無效的應用程式緩衝區類型 」。  
  
 如果 SQL_DESC_TYPE 在 IPD 記錄中設定為 SQL_SS_TABLE，而且對應的應用程式參數描述項記錄不是 SQL_C_DEFAULT，則會傳回 SQL_ERROR，並產生包含 SQLSTATE=HY003 以及「無效的應用程式緩衝區類型」的診斷記錄。 這可能會發生*ParameterType* SQLSetDescField、 SQLSetDescRec 或 SQLBindParameter。  
  
 如果*TargetType*呼叫 SQLGetData 時，參數為 SQL_SS_TABLE，則會傳回 SQL_ERROR，並診斷記錄會產生包含 SQLSTATE = HY003 以及 「 無效的應用程式緩衝區類型 」。  
  
 資料表值參數資料行無法當做 SQL_SS_TABLE 類型繫結。 如果**SQLBindParameter**呼叫*ParameterType*設定為 SQL_SS_TABLE，則會傳回 SQL_ERROR 並診斷記錄會產生包含 SQLSTATE = HY004 以及 「 無效的 SQL 資料類型 」。 這也會發生與 SQLSetDescField SQLSetDescRec。  
  
 資料表值參數資料行值與參數和結果資料行的資料轉換選項相同。  
  
 資料表值參數在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本中僅能是輸入參數。 如果嘗試將 SQL_DESC_PARAMETER_TYPE 設定為透過 SQLBindParameter 或 SQLSetDescField SQL_PARAM_INPUT 以外的值，會傳回 SQL_ERROR，而且診斷記錄加入至陳述式包含 SQLSTATE = HY105 和訊息 「 無效的參數型別 」。  
  
 資料表值參數資料行中無法使用 SQL_DEFAULT_PARAM *StrLen_or_IndPtr*，因為資料表值參數不支援每個資料列的預設值。 不過，應用程式會將資料行屬性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 設定為 1。 這表示資料行的所有資料列都會有預設值。 如果*StrLen_or_IndPtr*設定為 SQL_DEFAULT_PARAM，SQLExecute 或 SQLExecDirect 會傳回 SQL_ERROR，而且診斷的記錄將會加入至陳述式包含 SQLSTATE = HY090 和 「 無效的字串或緩衝區長度 」 訊息。  
  
## <a name="see-also"></a>請參閱＜  
 [資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
