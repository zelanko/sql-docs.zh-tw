---
title: SQLSetEnvAttr |Microsoft 文件
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
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 663d274b13a8cc5ac8ac53a2d8f9da4f925c7d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133942"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  [ODBC 程式設計人員參考](http://go.microsoft.com/fwlink/?LinkId=45250)定義如何解譯 ODBC 驅動程式應該**SQLSetEnvAttr**屬性從應用程式撰寫 ODBC 2 規格。*x*或 ODBC 3。*x*應用程式開發介面。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式符合這些規則。  
  
 其中一個屬性所控制**SQLSetEnvAttr**連接共用是否要使用。 如果連接共用搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式， *DriverCompletion*參數必須設定為 SQL_DRIVER_NOPROMPT，其中一種連接時[SQLDriverConnect](sqldriverconnect.md)或**SQLConnect**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetEnvAttr 函數](http://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  