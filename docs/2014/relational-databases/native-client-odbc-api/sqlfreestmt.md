---
title: SQLFreeStmt |Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9b7fbc3754121418ea2059ea511f3b247dcff8dd
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706097"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  在 ODBC 3.0 和更新版本中不建議使用**SQLFreeStmt** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援**SQLFreeStmt**所有已定義的*選項*值。 不過， [SQLCloseCursor](sqlclosecursor.md)、 [SQLBindParameter](sqlbindparameter.md)、 [SQLBindCol](sqlbindcol.md)、 **SQLSetDescField**和[SQLFreeHandle](sqlfreehandle.md)會取代或複製**SQLFreeStmt**的函式，因此應該改用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeStmt 函式](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
