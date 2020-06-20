---
title: SQLGetCursorName |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: rothja
ms.author: jroth
ms.openlocfilehash: 01ce6e42b4e8753d07309ec7ce298d4f743d4a6d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022275"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  如果應用程式未指定資料指標名稱， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會在資料指標產生時為應用程式產生一個。 應用程式可以使用**SQLGetCursorName**來抓取用於定位 UPDATE 和 DELETE 子句的驅動程式定義資料指標名稱。 應用程式不需要呼叫**SQLSetCursorName** ，即可利用定位的資料動作陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetCursorName 函式](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
