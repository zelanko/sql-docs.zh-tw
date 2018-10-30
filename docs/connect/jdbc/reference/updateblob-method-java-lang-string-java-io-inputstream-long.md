---
title: updateBlob 方法 (java.lang.String, java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 40f75549-5d5a-4de3-a271-4b8f0dd7b124
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eeedbd023fc6863f6bba75dfe9e1f41c83fd78c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597183"
---
# <a name="updateblob-method-javalangstring-javaioinputstream-long"></a>updateBlob 方法 (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的輸入資料流來更新指定的資料行，該值將包含指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
                                              long length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 **String**，包含資料行標籤。  
  
 *inputStream*  
  
 InputStream 物件。  
  
 *length*  
  
 **long**，指出資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 UpdateBlob 方法 java.sql.ResultSet 介面中所指定這個 updateBlob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateBlob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
