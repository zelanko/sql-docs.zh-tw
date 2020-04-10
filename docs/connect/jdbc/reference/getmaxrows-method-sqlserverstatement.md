---
title: getMaxRows 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fe813f8714bf9171873731cee68ac228dd3ace2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906864"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取最大資料列數目，即這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件產生 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件可以包含的資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出最大的資料列數目，如果沒有任何限制，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 getMaxRows 方法是由 java.sql.Statement 介面中的 getMaxRows 方法所指定。  
  
 這個 getMaxRows 方法一律會針對動態的可捲動資料指標傳回 0。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
