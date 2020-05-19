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
manager: craigg
ms.openlocfilehash: 7e9161170665d421b235a3a121ab8bb761e32daf
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706060"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  如果應用程式未指定資料指標名稱， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會在資料指標產生時為應用程式產生一個。 應用程式可以使用**SQLGetCursorName**來抓取用於定位 UPDATE 和 DELETE 子句的驅動程式定義資料指標名稱。 應用程式不需要呼叫**SQLSetCursorName** ，即可利用定位的資料動作陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetCursorName 函式](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
