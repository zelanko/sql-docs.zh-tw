---
title: jdbcCompliant 方法 (SQLServerDriver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0199a2cbbeb5f01472a17ade1575031c3ad994e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803213"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>jdbcCompliant 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  確認 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 是否符合 JDBC 規格。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>傳回值  
 如果 JDBC 驅動程式符合最小需求，則為 **true**； 否則為 **false**。  
  
## <a name="remarks"></a>Remarks  
 這個 jdbcCompliant 方法是由 java.sql.Driver 介面中 jdbcCompliant 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成員](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 類別](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
