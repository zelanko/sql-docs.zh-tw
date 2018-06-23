---
title: SQLExecDirect |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLExecDirect function
ms.assetid: e7c2a5b5-83f4-4c72-9aca-7b9fb4748b11
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7c51b1330f862dab23e028892945dce32f42d0e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146068"
---
# <a name="sqlexecdirect"></a>SQLExecDirect
  如果陳述式屬性 SQL_SOPT_SS_PARAM_FOCUS 不 0、 SQLExecDirect 會傳回 SQL_ERROR 並產生一個診斷記錄包含 SQLSTATE = HY024 及 「 無效的屬性值 SQL_SOPT_SS_PARAM_FOCUS （必須在執行階段的零） 」 的訊息。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=80709)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  