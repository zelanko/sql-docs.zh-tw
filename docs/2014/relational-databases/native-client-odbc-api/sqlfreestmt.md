---
title: SQLFreeStmt | Microsoft Docs
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
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8aa28af9291b06607021209fd673869b34157f53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136138"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt**建議您不要在 ODBC 3.0 和更新版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援所有定義*選項*值**SQLFreeStmt**。 不過， [SQLCloseCursor](sqlclosecursor.md)， [SQLBindParameter](sqlbindparameter.md)， [SQLBindCol](sqlbindcol.md)， **SQLSetDescField**，和[SQLFreeHandle](sqlfreehandle.md)取代或重複的函式**SQLFreeStmt**應改為使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeStmt 函數](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  