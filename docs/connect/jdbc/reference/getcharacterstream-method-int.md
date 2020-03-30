---
title: getCharacterStream 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getCharacterStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f9f230d-be4c-469a-b3dc-f24531429aae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0dd69211302a10fe72fc2742cbcd8b6bda7c933
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "68213691"
---
# <a name="getcharacterstream-method-int"></a>getCharacterStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取指定的資料行索引值來當作 java.io.Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getCharacterStream 方法是由 java.sql.ResultSet 介面中的 getCharacterStream 方法指定。  
  
 這個方法只會讀取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Unicode 字元資料類型，例如 nchar、nvarchar、nvarchar(max) 和 ntext。 所有其他資料型別 (包括 ASCII 字元型別) 將擲回例外狀況。 若要讀取 ASCII 資料類型，請使用 [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
