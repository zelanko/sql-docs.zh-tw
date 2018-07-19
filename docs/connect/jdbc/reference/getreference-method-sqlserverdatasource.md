---
title: getReference 方法 (SQLServerDataSource) |Microsoft 文件
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
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ec73d5918cebbc5a3c8ccd8261fc492717d8660
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32837153"
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將參考傳回給這[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>傳回值  
 參考物件。  
  
## <a name="remarks"></a>備註  
 這個 getReference 方法是由 javax.naming.Referenceable 介面中的 getReference 方法指定。  
  
 之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0 中，如果 SQLServerDataSource.setTrustStorePassword 在 SQLServerDataSource 物件上呼叫密碼會存在於 SQLServerDataSource.getReference，以便用來允許此物件所傳回的物件建立其他連接。 在 JDBC Driver 3.0 中，您需要在 SQLServerDataSource.getReference 傳回的物件上設定密碼，才能夠使用此物件建立連接。  
  
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
  
  
