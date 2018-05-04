---
title: 使用 SSL 加密連接 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86bdeaf93e6269294f15d98cbe0f0a0e88f5788b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-ssl-encryption"></a>使用 SSL 加密連接
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主題的範例描述如何在 Java 應用程式中使用連接字串屬性，好讓應用程式使用安全通訊端層 (SSL) 加密。 如需有關這些新的連接字串屬性例如**加密**， **trustServerCertificate**， **trustStore**， **trustStorePassword**，和**hostNameInCertificate**，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 當**加密**屬性設定為**true**和**trustServerCertificate**屬性設定為**，則為 true**、 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]將不會驗證[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證。 這是在測試環境中，例如位置允許連線通常需要進行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體有只有自我簽署的憑證。  
  
 下列程式碼範例示範如何設定**trustServerCertificate**連接字串中的屬性：  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 當**加密**屬性設定為**true**和**trustServerCertificate**屬性設定為**false**、 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]將驗證[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要驗證伺服器憑證，必須提供信任的資料在連接時使用**trustStore**和**trustStorePassword**連接屬性明確使用，或是使用基礎 Java Virtual Machine (JVM) 的預設信任存放區以隱含方式。  
  
 **TrustStore**屬性憑證 trustStore 檔案，其中包含的用戶端所信任的憑證清單中指定的路徑 （包括檔案名稱）。 **TrustStorePassword**屬性會指定用來檢查 trustStore 資料完整性的密碼。 如需有關使用 JVM 預設信任存放區的詳細資訊，請參閱[設定進行 SSL 加密用戶端](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)。  
  
 下列程式碼範例示範如何設定**trustStore**和**trustStorePassword**連接字串中的屬性：  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC 驅動程式提供一個額外的屬性**hostNameInCertificate**，以指定伺服器的主機名稱。 此屬性的值必須符合憑證的 Subject 屬性。  
  
 下列程式碼範例示範如何使用**hostNameInCertificate**連接字串中的屬性：  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  或者，您可以設定連接屬性的值，使用適當的**setter**所提供的方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。  
  
 如果**加密**屬性設定為**true**和**trustServerCertificate**屬性設定為**false**如果中的伺服器名稱連接字串中的伺服器名稱不相符[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證，會發出下列錯誤： 此驅動程式無法建立安全的連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用安全通訊端層 (SSL) 加密。 錯誤：「java.security.cert.CertificateException：無法在安全通訊端層 (SSL) 初始化期間驗證憑證中的伺服器名稱」。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)   
 [保護 JDBC Driver 應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
