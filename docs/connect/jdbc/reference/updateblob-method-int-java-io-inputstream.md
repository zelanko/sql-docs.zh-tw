---
title: updateBlob 方法 （int，java.io.InputStream） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d0263018-d326-4a7b-bf6f-5f508db899d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be97300d01a5f5ce7106f4225c30319ee0f42de7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642096"
---
# <a name="updateblob-method-int-javaioinputstream"></a>updateBlob 方法 (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的輸入資料流，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBlob(int columnIndex,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *inputStream*  
  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 UpdateBlob 方法 java.sql.ResultSet 介面中所指定這個 updateBlob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateBlob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
