---
title: prepareStatement 方法 (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5bb96dbe-f673-41b5-911b-8f661cca071a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b192f9055394393c48fa19eda697791ddfe3fa2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976167"
---
# <a name="preparestatement-method-javalangstring-int-int"></a>prepareStatement 方法 (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件，它會產生具有指定類型和並行的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sSql,  
                                                   int resultSetType,  
                                                   int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>參數  
 *sSql*  
  
 **String**，其中包含 SQL 陳述式。  
  
 *resultSetType*  
  
 **int**，指出結果集類型。  
  
 *resultSetConcurrency*  
  
 **int**，指出結果集的並行類型。  
  
## <a name="return-value"></a>傳回值  
 PreparedStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 prepareStatement 方法是由 java.sql.Connection 介面中的 prepareStatement 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 方法](../../../connect/jdbc/reference/sqlserverconnection-methods.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
