---
title: getMaxTablesInSelect 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxTablesInSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f5291217-2a0c-4daa-9e39-9f348fc911f7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c69570a365d27728e2cbaaac729b1bd824ba096
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906374"
---
# <a name="getmaxtablesinselect-method-sqlserverdatabasemetadata"></a>getMaxTablesInSelect 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在 SELECT 陳述式中使用的最大資料表數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxTablesInSelect()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大資料表數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 getMaxTablesInSelect 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxTablesInSelect 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
