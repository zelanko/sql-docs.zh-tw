---
title: updateNString 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6daca03f-c60f-4842-b9e3-11d136e78312
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b59df324948ff1d8745fc104fd9c4f7ffebd5b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834376"
---
# <a name="updatenstring-method-javalangstring-javalangstring"></a>updateNString 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的資料行標籤，使用 **String** 值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateNString(java.lang.String columnLabel,  
                          java.lang.String nString)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 **String**，包含資料行標籤。  
  
 *字串*  
  
 A**字串**物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 updateNString 方法是由 java.sql.ResultSet 介面中的 updateNString 方法指定。  
  
 此方法會傳遞 Java**字串**到所選**nchar**， **nvarchar （max)**， **ntext**，以及**xml**資料行。 在其他資料類型資料行上使用這個方法，將會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [updateNString 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
