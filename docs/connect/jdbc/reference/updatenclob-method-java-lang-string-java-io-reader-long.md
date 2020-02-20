---
title: updateNClob 方法 (java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ad5c8d9b-f8c8-4ddf-85c8-23420bba54ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a99434485ad244eec1f9cbb8ff4707e04f9d9907
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67998893"
---
# <a name="updatenclob-method-javalangstring-javaioreader-long"></a>updateNClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的 **Reader** 物件更新所指定資料行，該物件長度為指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 **String** 指出資料行標籤。  
  
 *reader*  
  
 Reader 物件。  
  
 *length*  
  
 參數資料中的字元數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateNClob 方法是由 java.sql.ResultSet 介面中的 updateNClob 方法指定。  
  
 只有在 **nvarchar(max)** 、**ntext** 和 **xml** 資料行上才支援這個方法。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [updateNClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
