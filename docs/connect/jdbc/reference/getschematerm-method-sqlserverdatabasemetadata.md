---
title: getSchemaTerm 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemaTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3e4a400f-0859-4ac3-983e-c25633b33683
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c45ad821b7fab27e51c2a6024c603d193257b7a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925409"
---
# <a name="getschematerm-method-sqlserverdatabasemetadata"></a>getSchemaTerm 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取慣用詞彙做為這個資料庫中的「目錄」。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getSchemaTerm()  
```  
  
## <a name="return-value"></a>傳回值  
 **String**，包含慣用詞彙。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSchemaTerm 方法是由 java.sql.DatabaseMetaData 介面中的 getSchemaTerm 方法指定。  
  
 當搭配 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 資料庫使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，這個方法會傳回作為慣用詞彙的 "schema"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
