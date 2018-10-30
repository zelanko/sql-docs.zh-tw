---
title: executeUpdate 方法 （) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0839ad771e067552b6c19d3d44c5893189a2c52d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782927"
---
# <a name="executeupdate-method-"></a>executeUpdate 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在這個 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件中執行的 SQL 陳述式必須是 SQL INSERT、UPDATE、MERGE 或 DELETE 陳述式；否則這個陳述式必須是不傳回任何項目的 SQL 陳述式，例如 DDL 陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>傳回值  
 **int** 會指出受影響的資料列數目，如果是使用 DDL 陳述式，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 executeUpdate 方法是由 java.sql.PreparedStatement 介面中的 executeUpdate 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [executeUpdate 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
