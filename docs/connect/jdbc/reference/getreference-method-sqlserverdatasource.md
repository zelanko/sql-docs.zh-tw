---
title: getReference 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4774dcda174d5260289409053a892cc4039b4f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980467"
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件的參考。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>傳回值  
 參考物件。  
  
## <a name="remarks"></a>Remarks  
 這個 getReference 方法是由 javax.xml.transform.dom.domresult 中的 getReference 方法指定。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 之前，如果 SQLServerDataSource.setTrustStorePassword 在 SQLServerDataSource 物件上呼叫，密碼會存在於 SQLServerDataSource.getReference 所傳回的物件中，以便允許使用此物件來建立其他連線。 在 JDBC Driver 3.0 中，您需要在 SQLServerDataSource.getReference 傳回的物件上設定密碼，才能夠使用此物件建立連接。  
  
 此外，如果您在繫結資料來源屬性之前設定 SQLServerDataSource.setTrustStorePassword，您必須先呼叫 SQLServerDataSource.setTrustStorePassword 才能取得連接。 例如，  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
