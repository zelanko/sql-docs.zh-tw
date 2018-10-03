---
title: locatorsUpdateCopy 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.locatorsUpdateCopy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6ec8c1d-7ff8-4bc5-8bd3-0199a9294a6e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e98a27b0afb23d0631d6d0bc0b5569324dea5d73
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758016"
---
# <a name="locatorsupdatecopy-method-sqlserverdatabasemetadata"></a>locatorsUpdateCopy 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出對 LOB 進行的更新作業是作用於複本或是直接作用於 LOB。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean locatorsUpdateCopy()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果更新作用於複本。 **false**如果直接進行更新。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 這個 locatorsUpdateCopy 方法是由 java.sql.DatabaseMetaData 介面中 locatorsUpdateCopy 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
