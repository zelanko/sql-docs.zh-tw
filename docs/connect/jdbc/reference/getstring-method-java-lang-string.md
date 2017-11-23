---
title: "getString 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getString (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6d9437a7fbba96fc92908fdd875dae964ee3bbb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getstring-method-javalangstring"></a>getString 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定之參數的值**字串**在 Java 程式語言中使用給定的參數名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數名稱。  
  
## <a name="return-value"></a>傳回值  
 A**字串**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getString 方法是由 java.sql.CallableStatement 介面中的 getString 方法來指定。  
  
 中的所有資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以當做字串傳回。 這表示可以傳回所有數字和字元類型的字串表示法以及二進位資料行的十六進位字串表示法，例如 binary、varbinary、varbinary(max)、image、timestamp 和 uniqueidentifier。  
  
 區分位置的型別 (例如 money、smallmoney、datetime、smalldatetime、float、real、decimal 和 numeric) 將會針對該型別的基礎值傳回標準 toString() 格式。  
  
 使用者定義型別會當做十六進位字串值傳回。  
  
## <a name="see-also"></a>請參閱＜  
 [getString 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
