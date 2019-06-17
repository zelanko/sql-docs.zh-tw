---
title: SQLGetCursorName | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 603a2b5be4ca75495f094aa838d0373a9689a523
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62657773"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  如果應用程式未指定資料指標名稱， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會產生一個在資料指標產生時為應用程式。 應用程式可以使用**SQLGetCursorName**擷取的驅動程式定義的資料指標名稱定位的 UPDATE 和 DELETE 陳述式。 應用程式不需要呼叫**SQLSetCursorName**利用位於資料操作陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetCursorName 函數](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
