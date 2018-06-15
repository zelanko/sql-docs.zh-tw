---
title: rowDeleted 方法 (SQLServerResultSet) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5a42409119b1d0e4280e36d417fd4d149b7625a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32841633"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出資料列是否已遭刪除。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果一個資料列已經刪除而且偵測到刪除則。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 rowDeleted 方法是由 java.sql.ResultSet 介面中的 rowDeleted 方法來指定。  
  
 刪除的資料列可能會在結果集中留下可見的漏洞。 這個方法可用來偵測結果集中的漏洞。 傳回的值取決於是否這[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件可以偵測到刪除。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 會偵測所有可更新的資料指標類型，已刪除的資料列，雖然偵測作業屬於暫時順向和動態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
