---
title: storesMixedCaseQuotedIdentifiers 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.storesMixedCaseQuotedIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1ffa599c-d0c8-43b6-8e9b-7c856a846630
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a997de47a565879009b5a21635bc61586f04e1d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838476"
---
# <a name="storesmixedcasequotedidentifiers-method-sqlserverdatabasemetadata"></a>storesMixedCaseQuotedIdentifiers 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理已加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成混合大小寫字母。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean storesMixedCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>傳回值  
 如果以混合大小寫字母的形式來儲存識別碼，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 storesMixedCaseQuotedIdentifiers 方法是由 java.sql.DatabaseMetaData 介面中 storesMixedCaseQuotedIdentifiers 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
