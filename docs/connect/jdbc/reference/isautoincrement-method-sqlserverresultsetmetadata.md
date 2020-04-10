---
title: isAutoIncrement 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isAutoIncrement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 028b8d61-9557-4c9f-b732-29e87a962de8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 314336220393eb05dab17164e33516c3740f24b7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909814"
---
# <a name="isautoincrement-method-sqlserverresultsetmetadata"></a>isAutoIncrement 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出指定之資料行是否已自動編號而形成唯讀狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isAutoIncrement(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 如果會自動將資料行編號，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isAutoIncrement 方法是由 java.sql.ResultSetMetaData 介面中的 isAutoIncrement 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
