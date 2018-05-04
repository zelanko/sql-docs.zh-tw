---
title: refreshRow 方法 (SQLServerResultSet) |Microsoft 文件
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
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50d89d95b5aecdd3ae430b278d83ab2222cde7d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="refreshrow-method-sqlserverresultset"></a>refreshRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用資料庫中的最新值來重新整理目前資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 refreshRow 方法是由 java.sql.ResultSet 介面中的 refreshRow 方法指定。  
  
 當資料指標位於插入資料列時，這個方法將無法進行呼叫。  
  
 這個方法會提供一種方法，讓應用程式明確地要求 JDBC Driver 從資料庫中重新提取資料列。 應用程式可能需要呼叫這個方法時[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]進行快取或預先提取從資料庫擷取資料列的最新的值。 如果提取大小大於 1，JDBC Driver 實際上可能需要同時重新提取多個資料列。  
  
 所有的值都會根據交易隔離等級和游標靈敏度進行重新提取。 如果之後呼叫 updater 方法，但會在呼叫之前呼叫這個方法[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法，對資料列的更新都會遺失。 經常呼叫這個方法可能會使效率變慢。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
