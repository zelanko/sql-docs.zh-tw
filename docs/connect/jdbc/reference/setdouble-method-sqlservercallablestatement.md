---
title: setDouble 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setDouble
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c054bb84-1292-4b70-b574-2ae189cd4e68
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b103bae2e7de26997545d0158ec2e3c440a0c59
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68213682"
---
# <a name="setdouble-method-sqlservercallablestatement"></a>setDouble 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 **double** 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setDouble(java.lang.String sCol,  
                      double d)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *d*  
  
 **double** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setDouble 方法是由 java.sql.CallableStatement 介面中的 setDouble 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
