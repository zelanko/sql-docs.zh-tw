---
title: "setTrustStorePassword 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d42539e3a0979500c28539d256226624ac6997eb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>setTrustStorePassword 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來檢查 trustStore 資料完整性的密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>參數  
 *trustStorePassword*  
  
 A**字串**其中包含用來檢查 trustStore 資料完整性的密碼。  
  
## <a name="remarks"></a>備註  
 trustStorePassword 屬性可以隨著 trustStore 屬性一起指定，而其值可用來檢查 trustStore 檔案的完整性。  
  
 如果有設定 trustStore 屬性，但是未設定 trustStorePassword 屬性，就不會檢查 trustStore 的完整性。  
  
 當 trustStore 和 trustStorePassword 屬性都未指定時，驅動程式將會使用 Java Virtual Machine (JVM) 系統屬性 "javax.net.ssl.trustStore" 和 "javax.net.ssl.trustStorePassword"。 如果未指定 "javax.net.ssl.trustStorePassword" 系統屬性，就不會檢查 trustStore 的完整性。  
  
 如果未設定 trustStore 屬性，但是有設定 trustStorePassword 屬性，JDBC 驅動程式將會使用 "javax.net.ssl.trustStore" 指定的檔案做為信任存放區，並使用指定的 trustStorePassword，檢查信任存放區的完整性。 當用戶端應用程式不要在 JVM 系統屬性中儲存密碼時，可能需要這個動作。  
  
 如需詳細資訊，請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 從 JDBC Driver 3.0 開始，如果您在繫結資料來源屬性之前設定 SQLServerDataSource.setTrustStorePassword，您必須先呼叫 SQLServerDataSource.setTrustStorePassword 才能取得連接。 如需詳細資訊，請參閱[SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

