---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7e597bcfa80d7d45064c844986018d64617d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190312"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt**不建議使用在 ODBC 3.0 和更新版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援所有定義*選項*的值**SQLFreeStmt**。 不過， [SQLCloseCursor](sqlclosecursor.md)， [SQLBindParameter](sqlbindparameter.md)， [SQLBindCol](sqlbindcol.md)， **SQLSetDescField**，和[SQLFreeHandle](sqlfreehandle.md)取代或重複的函式**SQLFreeStmt** ，應該改為使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeStmt 函數](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
