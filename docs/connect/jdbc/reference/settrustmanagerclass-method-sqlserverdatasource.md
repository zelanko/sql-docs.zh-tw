---
title: setTrustManagerClass 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setTrustManagerClass
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ae073d5adbc5a24b0afbb011bd4792cf09a5a94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809896"
---
# <a name="settrustmanagerclass-method-sqlserverdatasource"></a>setTrustManagerClass 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定 TrustManagerClass 連接屬性的字串值。
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTrustManagerClass(java.lang.String trustManagerClass)  
```  
  
#### <a name="parameters"></a>參數  
 *trustManagerClass*  
  
 A**字串**，其中包含自訂 javax.net.ssl.TrustManager 的完整的類別名稱。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
