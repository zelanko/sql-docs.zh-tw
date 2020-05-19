---
title: SQLExecDirect |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecDirect function
ms.assetid: e7c2a5b5-83f4-4c72-9aca-7b9fb4748b11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 36a5d580b6edb04f51d2fcf77dcc8ff0c8ba042f
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706142"
---
# <a name="sqlexecdirect"></a>SQLExecDirect
  如果語句屬性 SQL_SOPT_SS_PARAM_FOCUS 不是0，則 SQLExecDirect 會傳回 SQL_ERROR，並產生含有 SQLSTATE = HY024 的診斷記錄，以及訊息「不正確屬性值，SQL_SOPT_SS_PARAM_FOCUS （在執行時間必須為零）」。 如需 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=80709)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
