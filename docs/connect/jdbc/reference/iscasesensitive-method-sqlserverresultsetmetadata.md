---
title: isCaseSensitive 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isCaseSensitive
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4db67eb7-7ff2-4fb8-8052-39f699de53ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e40a9951cf148f6e5f37ee3286bb18753eeacd77
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928704"
---
# <a name="iscasesensitive-method-sqlserverresultsetmetadata"></a>isCaseSensitive 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出資料行是否區分大小寫。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isCaseSensitive(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 如果資料行會區分大小寫，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isCaseSensitive 方法是由 java.sql.ResultSetMetaData 介面中的 isCaseSensitive 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
