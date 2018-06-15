---
title: executeUpdate 方法 （) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a4d3caaa9cad0b1e9c47edece18015e6d270f1b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829494"
---
# <a name="executeupdate-method-"></a>executeUpdate 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行 SQL 陳述式中這[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)物件，它必須是 SQL INSERT、 UPDATE、 MERGE 或 DELETE 陳述式或傳回任何內容，例如 DDL 陳述式的 SQL 陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>傳回值  
 **int** 會指出受影響的資料列數目，如果是使用 DDL 陳述式，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 executeUpdate 方法是由 java.sql.PreparedStatement 介面中的 executeUpdate 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [executeUpdate 方法&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
