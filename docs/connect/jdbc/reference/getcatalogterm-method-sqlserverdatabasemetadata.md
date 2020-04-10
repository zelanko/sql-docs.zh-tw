---
title: getCatalogTerm 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0aa5d372-16aa-4790-a8f6-f8b742798f8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a639a8dd215df683ae603aac94c9f376eff278d6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924981"
---
# <a name="getcatalogterm-method-sqlserverdatabasemetadata"></a>getCatalogTerm 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取資料庫供應商的慣用詞彙做為「目錄」。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getCatalogTerm()  
```  
  
## <a name="return-value"></a>傳回值  
 包含目錄字詞的 **String**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 getCatalogTerm 方法由 java.sql.DatabaseMetaData 介面中的 getCatalogTerm 方法所指定。  
  
 當搭配 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 資料庫使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，這個方法會傳回 "database" 字詞。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
