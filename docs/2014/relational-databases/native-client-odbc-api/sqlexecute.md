---
title: SQLExecute |Microsoft 文件
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
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c422b06c23e2d8f42c48b3b7e03525e285db2769
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030778"
---
# <a name="sqlexecute"></a>SQLExecute
  如果陳述式屬性 SQL_SOPT_SS_PARAM_FOCUS 不會設定為 0，SQLExecute 會傳回 SQL_ERROR 並產生一個診斷記錄包含 SQLSTATE = HY024 及 「 無效的屬性值 SQL_SOPT_SS_PARAM_FOCUS （必須在執行階段的零） 」 的訊息。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
## <a name="remarks"></a>備註  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  