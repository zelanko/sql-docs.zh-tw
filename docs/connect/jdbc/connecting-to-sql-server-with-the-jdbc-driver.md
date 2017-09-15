---
title: "連接到 SQL Server JDBC driver |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ebc9542e5683eb58c198745892916893f284822
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>使用 JDBC 驅動程式連接到 SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  其中一個最基本動作，您將會執行與[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]是連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 所有與資料庫互動會透過[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)物件，而由於 JDBC 驅動程式擁有相當平面的架構，因此幾乎所有感興趣的行為都會用 SQLServerConnection 物件。  
  
 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]是只接聽 IPv6 通訊埠設定 java.net.preferIPv6Addresses 系統屬性，以確定 IPv6 而不是 IPv4 用來連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```  
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 本節中的主題描述如何建立及使用的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[建立連接 URL](../../connect/jdbc/building-the-connection-url.md)|描述如何產生連接 URL 以連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 也會說明連接到具名執行個體的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。|  
|[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)|描述各種連接屬性以及如何它們可以用於當您連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。|  
|[設定資料來源屬性](../../connect/jdbc/setting-the-data-source-properties.md)|描述如何在 Java Platform Enterprise Edition (Java EE) 環境中使用資料來源。|  
|[使用連接](../../connect/jdbc/working-with-a-connection.md)|描述要在其中建立連接到執行個體的各種方式[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。|  
|[使用連接共用](../../connect/jdbc/using-connection-pooling.md)|說明 JDBC 驅動程式如何支援使用連接共用。|  
|[使用資料庫鏡像 &#40;JDBC &#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|說明 JDBC 驅動程式如何支援使用資料庫鏡像。|  
|[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|描述如何開發將連接到 AlwaysOn 可用性群組的應用程式。|  
|[使用 Kerberos 整合式的驗證連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|討論其 Java 實作應用程式連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用 Kerberos 整合式的驗證。|  
|[連接到 Azure SQL database](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|討論 SQL Azure 上資料庫的連接問題。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
