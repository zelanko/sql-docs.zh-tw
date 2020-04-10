---
title: jdbcCompliant 方法 (SQLServerDriver) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ae5ac88d0427a605493bc19786bdd5f23dc93b6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915060"
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
  
## <a name="remarks"></a>備註  
 這個 jdbcCompliant 方法是由 java.sql.Driver 介面中的 jdbcCompliant 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成員](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 類別](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
