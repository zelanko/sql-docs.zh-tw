---
title: getSchemaName 方法 (SQLServerResultSetMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getSchemaName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2d0063ab-d5d7-420f-b388-36d5169b1358
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69e5183ceea19693205dc7f30a97e29bfb2bb70d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980139"
---
# <a name="getschemaname-method-sqlserverresultsetmetadata"></a>getSchemaName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取得指定之資料行的資料表結構描述名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getSchemaName(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 包含結構描述名稱的 **String**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getSchemaName 方法是由 ResultSetMetaData 介面中的 getSchemaName 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
