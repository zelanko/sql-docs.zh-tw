---
title: updateNString 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6daca03f-c60f-4842-b9e3-11d136e78312
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41c12f32b1b42153baa79543ca284872040763ba
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040866"
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
  
  
