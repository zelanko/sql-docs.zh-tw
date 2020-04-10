---
title: getTimestamp 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d5174db-365c-4476-9472-7871578ef34c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c2c6530e6df31502841ad931852f317a2e838b7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924513"
---
# <a name="gettimestamp-method-javalangstring"></a>getTimestamp 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在 Java 程式語言中使用給定的參數名稱，擷取指定之參數的值來當做 java.sql.Timestamp 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 Timestamp 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTimestamp 方法是由 java.sql.CallableStatement 介面中的 getTimestamp 方法指定。  
  
 這個方法只會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 和 **smalldatetime** 資料行中的值。  
  
## <a name="see-also"></a>另請參閱  
 [getTimestamp 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
