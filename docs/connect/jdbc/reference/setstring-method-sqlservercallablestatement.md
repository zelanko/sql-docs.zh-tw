---
title: "setString 方法 (SQLServerCallableStatement) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ebcac5fedd89cbec614d7278232c3a5e32e5740
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-sqlservercallablestatement"></a>setString 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的 Java**字串**值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數的名稱。  
  
 *s*  
  
 A**字串**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetString 方法 java.sql.CallableStatement 介面中所指定此 setString 方法。  
  
 執行字串到二進位的轉換時，才[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]知道目標類型是二進位。 在 JDBC 驅動程式不知道基礎類型的情況下，它會通過**字串**常值和傳回伺服器錯誤，如果伺服器無法執行轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

