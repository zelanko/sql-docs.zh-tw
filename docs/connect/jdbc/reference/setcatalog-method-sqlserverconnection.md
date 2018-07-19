---
title: setCatalog 方法 (SQLServerConnection) |Microsoft 文件
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
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91597c7a995fb0ecf810d3b0f58760c12784564e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842203"
---
# <a name="setcatalog-method-sqlserverconnection"></a>setCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定指定的目錄名稱來選取這個子[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)中用來工作的物件的資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>參數  
 *catalog*  
  
 A**字串**，其中包含目錄名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setCatalog 方法是由 java.sql.Connection 介面中的 setCatalog 方法來指定。  
  
 *目錄*引數會由逸出[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]自動。 使用此方法會設定連接物件的 catalog 屬性。 它不會以任何其他方式進行隱含設定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
