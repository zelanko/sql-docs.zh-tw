---
title: registerOutParameter 方法加入類型 |Microsoft 文件
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
- SQLServerCallableStatement.registerOutParameter (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d00242c-4d9c-42cc-86bb-b76f5ef876b8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c83e1cbca20e3b60c358894a68af3b950165e69
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="registeroutparameter-method-javalangstring-int"></a>registerOutParameter 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  向給定 JDBC 型別的指定參數註冊 OUT 參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n)  
```  
  
#### <a name="parameters"></a>參數  
 *S*  
  
 包含參數名稱的**字串**。  
  
 *n*  
  
 JDBC 型別程式碼，如 java.sql.Types 中所定義。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 registerOutParameter 方法是由 java.sql.CallableStatement 介面中的 registerOutParameter 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [registerOutParameter 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
