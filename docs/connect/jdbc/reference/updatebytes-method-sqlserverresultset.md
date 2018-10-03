---
title: updateBytes 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3050c836-fbb3-4475-99e5-05637a48a932
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c58b9198e3e5472a27b37ab36f4a7747c33eef12
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755137"
---
# <a name="updatebytes-method-sqlserverresultset"></a>updateBytes 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 **byte** 值的陣列，更新指定的資料行。  
  
## <a name="overload-list"></a>多載清單  
  
|[屬性]|Description|  
|----------|-----------------|  
|[updateBytes (int, byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-int-byte.md)|根據指定的資料行索引，使用 **byte** 值的陣列來更新指定的資料行。|  
|[updateBytes (java.lang.String, byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-java-lang-string-byte.md)|根據指定的資料行名稱，使用 **byte** 值的陣列來更新指定的資料行。|  
  
## <a name="remarks"></a>Remarks  
 在舊版的 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 中，您可以使用 SQLServerResultSet.updateBytes 來轉換位元組陣列與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 **date**、**time**、**datetime2** 或 **datetimeoffset** 之間的值。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
