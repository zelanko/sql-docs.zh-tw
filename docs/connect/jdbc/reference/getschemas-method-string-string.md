---
title: getSchemas 方法 （String，String） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76c5831547178b33854465d38cfe97dc87684d15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684606"
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
  
 在資料庫中之目錄的名稱。 如果它是空字串 ""，結果就會包含結構描述而不包含目錄。 如果它是 **null**，目錄名稱就不會用於搜尋。  
  
 *schemaPattern*  
  
 結構描述的名稱。 如果它是 **null**，結構描述名稱就不會用於搜尋。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getSchemas 方法是由 java.sql.DatabaseMetaData 介面中的 getSchemas 方法指定。  
  
 透過 getSchemas 方法所傳回的結果集將包含下列資訊：  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|結構描述的名稱。|  
|TABLE_CATALOG|**String**|結構描述的目錄名稱。|  
  
 這些結果會依據 TABLE_CATALOG 排列，接著再依據 TABLE_SCHEM 排列。 每個資料列都是以 TABLE_SCHEM 做為第一個資料列，以 TABLE_CATALOG 做為第二個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
