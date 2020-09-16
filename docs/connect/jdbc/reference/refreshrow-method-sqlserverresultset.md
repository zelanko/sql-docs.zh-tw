---
description: refreshRow 方法 (SQLServerResultSet)
title: refreshRow 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67a472b8bf87d8a51e2999d9285bcfa818ade134
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432810"
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
  
 這個方法會提供一種方法，讓應用程式明確地要求 JDBC Driver 從資料庫中重新提取資料列。 當 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 進行快取或預先提取，以便從資料庫中提取最新資料列值的時候，應用程式可能需要呼叫這個方法。 如果提取大小大於 1，JDBC Driver 實際上可能需要同時重新提取多個資料列。  
  
 所有的值都會根據交易隔離等級和游標靈敏度進行重新提取。 如果是在呼叫 updater 方法之後，且在呼叫 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法之前呼叫這個方法，則對資料列完成的更新會遺失。 經常呼叫這個方法可能會使效率變慢。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
