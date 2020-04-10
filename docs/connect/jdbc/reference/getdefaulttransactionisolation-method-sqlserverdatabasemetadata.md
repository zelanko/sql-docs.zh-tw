---
title: getDefaultTransactionIsolation 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDefaultTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85b867ed-de5a-4879-b3f8-bce897879077
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 58be916063f1bd0893285c6c893241e3ec4e699f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80917712"
---
# <a name="getdefaulttransactionisolation-method-sqlserverdatabasemetadata"></a>getDefaultTransactionIsolation 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫的預設交易隔離等級。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getDefaultTransactionIsolation()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出預設的交易隔離等級。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getDefaultTransactionIsolation 方法是由 java.sql.DatabaseMetaData 介面中的 getDefaultTransactionIsolation 方法所指定。  
  
 當搭配 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 資料庫使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，這個方法會傳回值 TRANSACTION_READ_COMMITTED 或是 **int** 值 2。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
