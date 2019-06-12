---
title: Building the Connection URL |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0d9d79d6462300df8b96fa3ec58349c39e751cf
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770264"
---
# <a name="building-the-connection-url"></a>建立連接 URL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  連接 URL 的一般格式為  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 其中：  
  
-   **jdbc:sqlserver://** (必要項) 也就是子通訊協定，且為常數。  
  
-   **serverName** (選擇項) 是要連線的伺服器位址。 此項可以是 DNS 或 IP 位址，或也可以是本機電腦的 localhost 或 127.0.0.1。 如果未在連接 URL 中指定，就必須在屬性集合中指定伺服器名稱。  
  
-   **instanceName** (選擇項) 是 serverName 上要連線的執行個體。 如果未指定，將會連接到預設執行個體。  
  
-   **portNumber** (選擇項) 是 serverName 上要連線的連接埠。 預設值是 1433。 如果您使用預設值，則不需在 URL 中指定連接埠，也不需指定前面的 ':'。  
  
    > [!NOTE]  
    >  若要達到最佳的連接效能，在連接到具名執行個體時應設定 portNumber。 如此可避免為了判斷通訊埠號碼而徒勞往返於伺服器。 如果同時使用 portNumber 及 instanceName，將優先使用 portNumber 並忽略 instanceName。  
  
-   **property** (選擇項) 是一或多個選項連線屬性。 如需詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。 可以指定清單中的任何屬性。 屬性只能使用分號 (';') 來分隔，且不能重複。  
  
> [!CAUTION]  
>  為了安全起見，您應該避免根據使用者輸入來建立連接 URL。 應該只在 URL 中指定伺服器名稱和驅動程式。 至於使用者名稱和密碼值，請使用連接屬性集合。 如需 JDBC 應用程式的安全性的詳細資訊，請參閱[保護的 JDBC 驅動程式應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)。  
  
## <a name="connection-examples"></a>連接範例  
 使用一個使用者名稱及密碼，連接至本機電腦上的預設資料庫：  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  雖然先前的範例是在連接字串中使用使用者名稱及密碼，但是您應該使用整合式安全性，因為它更安全。 如需詳細資訊，請參閱本主題稍後的[使用整合式驗證連線](#Connectingintegrated)。  
  
 下列連接字串示範如何從 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援的任何作業系統上執行的應用程式，使用整合式驗證和 Kerberos 連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫：  
  
```java
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 使用整合式驗證，連接到本機電腦上的預設資料庫：  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 連接到遠端伺服器上的具名資料庫：  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 以預設通訊埠連接到遠端伺服器：  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 指定自訂的應用程式名稱以進行連接：  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>具名和多個 SQL Server 執行個體  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許在每部伺服器上安裝多個資料庫執行個體。 並以特定的名稱識別每個執行個體。 若要連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體，您可以指定具名執行個體的連接埠號碼 (偏好選項)，或者將執行個體名稱指定為 JDBC URL 屬性或 **datasource** 屬性。 如果沒有指定執行個體名稱或通訊埠號碼屬性，則會建立預設執行個體的連接。 請參閱下列範例：  
  
 若要使用通訊埠號碼，請執行下列：  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 若要使用 JDBC URL 屬性，請執行下列動作：  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>連接 URL 中的逸出值  
 因為包含了空格、分號和引號這類特殊字元，可能有需要逸出連接 URL 值中的特定部份。 如果字元是內含在大括弧中，JDBC 驅動程式就支援逸出這些字元。 例如，{;} 可逸出分號。  
  
 逸出值可以包含特殊字元 (特別是 '='、';'、'[]' 和空格)，但不能包含大括弧。 必須逸出和包含大括弧的值，應該加入屬性集合中。  
  
> [!NOTE]  
>  大括弧內的空格是常值，不會被修剪。  
  
##  <a name="Connectingintegrated"></a> 在 Windows 上使用整合式驗證連線  
 JDBC 驅動程式支援在 Windows 作業系統上使用類型 2 整合式驗證，方法是透過 integratedSecurity 連接字串屬性。 若要使用整合式驗證，請將 sqljdbc_auth.dll 檔複製到安裝 JDBC 驅動程式的電腦上 Windows 系統路徑中的目錄。  
  
 sqljdbc_auth.dll 檔會安裝在下列位置：  
  
 \<*installation directory*>\sqljdbc_\<*version*>\\<*language*>\auth\  
  
 適用於任何支援的作業系統[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，請參閱 <<c2> [ 使用 Kerberos 整合式驗證來連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)如需在中新增一項功能的描述[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，可讓應用程式連接到透過類型 4 Kerberos 整合式的驗證的資料庫。  
  
> [!NOTE]  
>  如果您執行的是 32 位元的 Java Virtual Machine (JVM)，即使作業系統為 x64 版，也請使用 x86 資料夾中的 sqljdbc_auth.dll 檔案。 如果您是在 x64 處理器上執行 64 位元的 JVM，請使用 x64 資料夾中的 sqljdbc_auth.dll 檔案。  
  
 或者，您也可以設定 java.libary.path 系統屬性來指定 sqljdbc_auth.dll 的目錄。 例如，如果 JDBC Driver 安裝在預設目錄中，您就可以在 Java 應用程式啟動時，使用下列虛擬機器 (VM) 引數來指定 DLL 的位置：  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>以 IPv6 位址連接  
 JDBC 驅動程式支援使用 IPv6 位址搭配連接屬性集合，以及搭配 serverName 連接字串屬性。 連接字串中的 IPv6 位址不支援初始 serverName 值，例如 jdbc:sqlserver  ://serverName  。 針對 *serverName* 請使用名稱，而不要使用原始 IPv6 位址，此方法適用於所有的連線情況。 下列範例提供詳細資訊。  
  
 **使用 serverName 屬性**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **使用屬性集合**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
