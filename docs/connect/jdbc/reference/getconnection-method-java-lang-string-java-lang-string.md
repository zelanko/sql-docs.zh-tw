---
title: "getConnection 方法 （java.lang.String，java.lang.String） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 39b7a3bb2896ff308fc58510443bd54c487c77f8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試建立連接的資料來源這個[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件代表使用指定的使用者名稱和密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>參數  
 *使用者名稱*  
  
 A**字串**，其中包含使用者名稱。  
  
 *密碼*  
  
 A**字串**其中包含的密碼。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 GetConnection 方法，這是由 getConnection 方法，由 javax.sql.DataSource 介面中指定。  
  
 呼叫 getConnection 方法，使用非 null 使用者名稱或密碼將會取代初始化 SQLServerConnection 物件時，SQLServerDataSource 類別上所設定的使用者名稱和密碼屬性。 例如，如果呼叫端已呼叫[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)和[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)上資料來源，然後呼叫 getConnection 並提供非 null 使用者名稱或非 null 密碼，使用者名稱和密碼設定setUser 和 setPassword 將被取代的使用者名稱和密碼傳遞至 getConnection。  
  
> [!NOTE]  
>  使用者名稱和密碼所使用的呼叫在 URL 內設定[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)方法不會在此情況下變更。  
  
## <a name="see-also"></a>另請參閱  
 [getConnection 方法 &#40;SQLServerDataSource &#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
