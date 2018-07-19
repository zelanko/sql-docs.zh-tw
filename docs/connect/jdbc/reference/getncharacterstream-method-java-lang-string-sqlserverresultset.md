---
title: getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a117f3a3-9c25-41e1-9adb-a40e90620dd6
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83904018dc16b2a074b77b4e88d91a8222ef4417
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836113"
---
# <a name="getncharacterstream-method-javalangstring-sqlserverresultset"></a>getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 字串，包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetNCharacterStream 方法 java.sql.ResultSet 介面中所指定此 getNCharacterStream 方法。  
  
 這個方法可以用來擷取值的**nvarchar**， **nchar**， **nvarchar （max)**， **ntext**，或**xml**中目前資料列，這個資料行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。 如果嘗試使用這個方法來擷取其他資料類型的值，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNCharacterStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
