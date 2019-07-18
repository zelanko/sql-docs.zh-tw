---
title: isClosed 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e79b5b53-16b0-42a3-be4e-542a77a21e12
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e801fe11bcf26fd474290f7cac8c660b40e5b0b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796558"
---
# <a name="isclosed-method-sqlserverstatement"></a>isClosed 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件是否已關閉。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>傳回值  
 如果這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件已關閉，則為 **true**；如果仍為開啟，則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isClosed 方法是由 java.sql.Statement 介面中的 isClosed 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
