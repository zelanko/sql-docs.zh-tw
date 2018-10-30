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
manager: craigg
ms.openlocfilehash: 9f82cbfee67acdb914263bd2fe70e0388f86a7f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695086"
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
  
 讀取器物件。  
  
 *length*  
  
 參數資料中的字元數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 UpdateNClob 方法 java.sql.ResultSet 介面中所指定這個 updateNClob 方法。  
  
 這個方法僅支援**nvarchar （max)**， **ntext**，並**xml**資料行。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [updateNClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
