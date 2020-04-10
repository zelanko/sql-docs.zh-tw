---
title: getConnection 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f520e96-5313-468f-b987-535ddaea027e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714ba26610aa27fbc05cb27156b293c13e58130d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923323"
---
# <a name="getconnection-method-"></a>getConnection 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試與這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件所代表的資料來源建立連線。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>傳回值  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getConnection 方法是由 javax.sql.DataSource 介面中的 getConnection 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [getConnection 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
