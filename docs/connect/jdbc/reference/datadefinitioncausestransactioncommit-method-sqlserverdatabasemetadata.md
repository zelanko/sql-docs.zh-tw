---
title: 資料定義陳述式強制交易未認可。 | Microsoft Docs
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
- SQLServerDatabaseMetaData.dataDefinitionCausesTransactionCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf04fa73-b9f1-4403-b6a0-e53d0d27c671
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d0978c314464e5d4f60d2247e090377bf7bb3d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32828783"
---
# <a name="datadefinitioncausestransactioncommit-method-sqlserverdatabasemetadata"></a>dataDefinitionCausesTransactionCommit 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出交易中的資料定義陳述式是否會強制交易進行認可。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean dataDefinitionCausesTransactionCommit()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果 DDL 陳述式強制認可。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 dataDefinitionCausesTransactionCommit 方法是由 java.sql.DatabaseMetaData 介面中 dataDefinitionCausesTransactionCommit 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
