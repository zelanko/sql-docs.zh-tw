---
title: getBytes 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1369c40e071d6045bdf42b6c425fb4b94932cf08
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655578"
---
# <a name="getbytes-method-sqlservercallablestatement"></a>getBytes 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的值來當做位元組陣列。  
  
## <a name="overload-list"></a>多載清單  
  
|[屬性]|Description|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int.md)|透過給定的參數索引，擷取指定之參數的值來當做位元組值的陣列。|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|透過給定的參數名稱，擷取指定之參數的值來當做位元組值的陣列。|  
  
## <a name="remarks"></a>Remarks  
 在舊版的 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 中，您可以使用 SQLServerCallableStatement.setBytes 來轉換位元組陣列與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 **date**、**time**、**datetime2** 或 **datetimeoffset** 之間的值。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
