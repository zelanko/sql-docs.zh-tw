---
title: SQLServerStatement 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7488efcb3392623e6f54cff440a16494c10e0a69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705346"
---
# <a name="sqlserverstatement-class"></a>SQLServerStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 陳述式功能的基本實作。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：**[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerStatement 類別也針對 JDBC 備妥及可呼叫的陳述式提供許多基底類別實作方法。 SQLServerStatement 類別的基本角色是執行 SQL 陳述式，然後將更新計數和結果集傳回給使用者應用程式。  
  
 此類別支援解除包裝成為 SQLServerStatement 類別、 ISQLServerStatement 介面和 java.sql.Statement 介面。 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
