---
title: isDefinitelyWritable 方法 (SQLServerResultSetMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isDefinitelyWritable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7650e89a-dc8e-43ca-8eb2-f962f1a4b4ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d8424b15035559b0c6fb2d6c03ced22e4f45677
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637246"
---
# <a name="isdefinitelywritable-method-sqlserverresultsetmetadata"></a>isDefinitelyWritable 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出寫入至所指定資料行的作業是否絕對會成功。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isDefinitelyWritable(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 如果資料行寫入絕對會成功，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isDefinitelyWritable 方法是由 java.sql.ResultSetMetaData 介面中 isDefinitelyWritable 方法指定。  
  
> [!NOTE]  
>  當配合 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫使用 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 時，這個方法一律會傳回 false。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
