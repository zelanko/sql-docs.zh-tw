---
title: supportsCoreSQLGrammar 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCoreSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6b82f300-f906-4d11-b810-525bda4a88ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6bc18cd7c49a2dae98c20e28f1e0789f260ea59f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928132"
---
# <a name="supportscoresqlgrammar-method-sqlserverdatabasemetadata"></a>supportsCoreSQLGrammar 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否支援 ODBC Core SQL 文法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsCoreSQLGrammar()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsCoreSQLGrammer 方法是由 java.sql.DatabaseMetaData 介面中的 supportsCoreSQLGrammer 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
