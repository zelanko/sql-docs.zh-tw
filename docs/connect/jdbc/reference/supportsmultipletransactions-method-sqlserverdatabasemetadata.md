---
title: supportsMultipleTransactions 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMultipleTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 34ff8dcb-5487-46d1-a4c1-25e33eb3eee4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ab606d2898cd6792ad53dd3221e0c05f6f08b1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810746"
---
# <a name="supportsmultipletransactions-method-sqlserverdatabasemetadata"></a>supportsMultipleTransactions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否允許在不同連接上一次開啟多個交易。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsMultipleTransactions()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果支援。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 supportsMultipleTransactions 方法是由 java.sql.DatabaseMetaData 介面中 supportsMultipleTransactions 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
