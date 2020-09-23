---
title: 使用 JDBC 驅動程式連線到 SQL Server | Microsoft Docs
description: 使用 Microsoft JDBC Driver for SQL Server 連線到資料庫時，所有與該資料庫的互動都會經由 SQLServerConnection 物件。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88a1bbe3554b74e3dae67ddb1fad93122fc41fe
ms.sourcegitcommit: 822d4b3cfa53269535500a3db5877a82b5076728
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87988622"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>使用 JDBC 驅動程式連線到 SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  您將使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 進行的其中一項最基本動作就是連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 所有與資料庫的互動都是經由 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 物件發生，而且因為 JDBC 驅動程式擁有這類平面架構，所以幾乎所有令人關注的行為都會用到 SQLServerConnection 物件。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只接聽 IPv6 連接埠，請設定 java.net.preferIPv6Addresses 系統屬性，以確保使用 IPv6 而不是 IPv4 來連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 本節的主題描述如何建立和使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的連線。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[建置連線 URL](../../connect/jdbc/building-the-connection-url.md)|描述如何產生連線 URL 以連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 也會描述連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的具名執行個體。|  
|[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)|描述各種連線屬性，以及它們在連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫時的使用方式。|  
|[設定資料來源屬性](../../connect/jdbc/setting-the-data-source-properties.md)|描述如何在 Java Platform Enterprise Edition (Java EE) 環境中使用資料來源。|  
|[使用連線](../../connect/jdbc/working-with-a-connection.md)|描述各種建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫連線執行個體的方法。|  
|[使用連接共用](../../connect/jdbc/using-connection-pooling.md)|說明 JDBC 驅動程式如何支援使用連接共用。|  
|[使用資料庫鏡像 &#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|說明 JDBC 驅動程式如何支援使用資料庫鏡像。|  
|[JDBC 驅動程式對於高可用性、災害復原的支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|描述如何開發將連接到 AlwaysOn 可用性群組的應用程式。|  
|[使用 Kerberos 整合式驗證連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|針對使用 Kerberos 整合式驗證連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的應用程式討論其 Java 實作。|  
|[連接到 Azure SQL Database](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|討論 Azure SQL 上資料庫的連線問題。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
