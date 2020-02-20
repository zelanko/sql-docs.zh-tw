---
title: getFunctions 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b799fb56207294041c52fe455ad2acceff508d3a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982951"
---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>getFunctions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取系統和使用者函數的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>參數  
 *catalog*  
  
 在資料庫中之目錄的名稱。 如果它是空字串 ""，結果就會包含函數而不包含目錄。 如果它是 **null**，目錄名稱就不會用於搜尋。  
  
 *schemaPattern*  
  
 結構描述的名稱。 如果它是空字串 ""，結果就會包含函數而不包含結構描述。 如果它是 **null**，結構描述名稱就不會用於搜尋。  
  
 *functionNamePattern*  
  
 函數的名稱。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getFunctions 方法是由 java.sql.DatabaseMetaData 介面中的 getFunctions 方法指定。  
  
 這個方法只會傳回符合指定之結構描述和函數名稱的系統和使用者函數。  
  
> [!IMPORTANT]  
>  傳回的結果集可能會包含呼叫使用者時並不具備執行權限的函數。  
  
 每個函數描述都包括下列資料行：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|函數所在之資料庫的名稱。|  
|FUNCTION_SCHEM|**String**|函數所在之結構描述的名稱。|  
|FUNCTION_NAME|**String**|函數的名稱。|  
|NUM_INPUT_PARAMS|**int**|保留供日後使用，目前會傳回值 -1。|  
|NUM_OUTPUT_PARAMS|**int**|保留供日後使用，目前會傳回值 -1。|  
|NUM_RESULT_SETS|**int**|保留供日後使用，目前會傳回值 -1。|  
|REMARKS|**String**|有關此函數的註解。|  
|FUNCTION_TYPE|**short**|函數的類型。 它可能是下列其中一個值：<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 在所傳回結果集中的所有描述，都會依據 FUNCTION_CAT、FUNCTION_SCHEM、FUNCTION_NAME 和 SPECIFIC_NAME 排列順序。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
