---
title: getSchemas 方法 （String，String） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0684e2ec5e840d6fbe2f45cdcb66f39feb404320
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getschemas-method-string-string"></a>getSchemas 方法 (String, String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的目錄名稱和結構描述名稱，擷取目前資料庫中所提供的結構描述名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public ResultSet getSchemas(java.lang.String catalog,  
                       java.lang.String schemaPattern)  
```  
  
#### <a name="parameters"></a>參數  
 *catalog*  
  
 在資料庫中之目錄的名稱。 如果它是空字串 ""，結果就會包含結構描述而不包含目錄。 如果是**null**，目錄名稱不會用於搜尋。  
  
 *schemaPattern*  
  
 結構描述的名稱。 如果是**null**，結構描述名稱不會用於搜尋。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetSchemas 方法 java.sql.DatabaseMetaData 介面中所指定此 getSchemas 方法。  
  
 GetSchemas 方法所傳回的結果集包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**字串**|結構描述的名稱。|  
|TABLE_CATALOG|**字串**|結構描述的目錄名稱。|  
  
 這些結果會依據 TABLE_CATALOG 排列，接著再依據 TABLE_SCHEM 排列。 每個資料列都是以 TABLE_SCHEM 做為第一個資料列，以 TABLE_CATALOG 做為第二個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
