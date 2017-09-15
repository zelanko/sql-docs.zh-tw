---
title: "應用程式安全性 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e608d2181520284be87dbdaa078ff261a2a7d878
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="application-security"></a>應用程式安全性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，請務必採取預防措施以確保您的應用程式的安全性。 下列章節會提供保護應用程式時可採取之步驟的相關資訊。  
  
## <a name="using-java-policy-permissions"></a>使用 Java 原則權限  
 當您使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，請務必指定 JDBC 驅動程式需要的必要的 Java 原則權限。 Java Runtime Environment (JRE) 提供您可在執行階段時使用的延伸安全性模型，以判斷執行緒是否具有資源的存取權限。 安全性原則檔可控制這個存取權限。 原則檔本身是由部署人員和容器的系統管理員所管理，但本主題列出的權限則會影響 JDBC 驅動程式的功能。  
  
 原則檔中典型的權限看起來如下：  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 下列程式碼基底應該限制為 JDBC 驅動程式程式碼基底，以確定您授與最少量的權限。  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  程式碼 "file:/install_dir/lib/-" 是指 JDBC 驅動程式的安裝目錄。  
  
## <a name="protecting-server-communication"></a>保護伺服器通訊  
 當您使用 JDBC 驅動程式與通訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫，您可以藉由使用網際網路通訊協定安全性 (IPSEC) 或安全通訊端層 (SSL)，保護通訊通道，或同時使用兩者。  
  
 SSL 支援可以用於提供 IPSEC 之外的其他保護等級。 如需有關使用 SSL 的詳細資訊，請參閱[使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)。  
  
## <a name="see-also"></a>另請參閱  
 [保護 JDBC 驅動程式應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
