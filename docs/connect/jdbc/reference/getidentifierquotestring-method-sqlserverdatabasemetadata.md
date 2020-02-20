---
title: getIdentifierQuoteString 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIdentifierQuoteString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dea35a0-56a8-412c-8cd3-6539527ff597
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe27259efbc3448fd0d8d4350d0c2e93e906c34a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982856"
---
# <a name="getidentifierquotestring-method-sqlserverdatabasemetadata"></a>getIdentifierQuoteString 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取用來引用 SQL 識別碼的**字串**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getIdentifierQuoteString()  
```  
  
## <a name="return-value"></a>傳回值  
 包含引號識別碼的**字串**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getIdentifierQuoteString 方法是由 java.sql.DatabaseMetaData 介面中的 getIdentifierQuoteString 方法所指定。  
  
 當您搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫使用 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] JDBC Driver 時，這個方法會傳回 **double** 引號 ("")。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
