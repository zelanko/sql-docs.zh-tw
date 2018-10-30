---
title: getMaxConnections 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxConnections
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 745410f7-e59b-4423-9728-c903adedc399
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bda30a06bd2d6325dbbce4f06c7f8e50bbc93c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838946"
---
# <a name="getmaxconnections-method-sqlserverdatabasemetadata"></a>getMaxConnections 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫可能建立的最大並行連接數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxConnections()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大並行連線數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getMaxConnections 方法是由 java.sql.DatabaseMetaData 介面中 getMaxConnections 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
