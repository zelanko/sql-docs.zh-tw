---
title: "功能相依性的 Microsoft JDBC Driver for SQL Server |Microsoft 文件"
ms.custom: 
ms.date: 02/28/2018
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
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 703a27220a80744c46ca0bc7667756cec1ab6596
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能相依性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

 此頁面包含 Microsoft JDBC Driver for SQL Server 取決於程式庫的清單。 專案有下列的相依性。
 
 ## <a name="compile-time"></a>編譯時間
 - `azure-keyvault` ： （選擇性） 一律加密 Azure 金鑰保存庫功能 azure 金鑰保存庫提供者
 - `adal4j` : Azure ActiveDirectory Library for Java 的 Azure Active Directory 驗證功能和 Azure 金鑰保存庫的功能 （選擇性）

 ##  <a name="test-time"></a>測試時間
其中一個上述兩項功能需要的特定專案需要明確宣告其 pom 檔案中的個別相依性：

***例如：***如果您使用*Azure Active Directory 驗證功能*，則您需要重新宣告*adal4j*您的專案 pom 檔案中的相依性。 下列程式碼片段，請參閱： 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>
```

***例如：***如果您使用*Azure 金鑰保存庫功能*則需要重新宣告*azure keyvault*相依性和*adal4j*中的相依性您專案的 pom 檔案。 下列程式碼片段，請參閱： 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```
 
 ## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 驅動程式的相依性需求

 ### <a name="azure-keyvault-feature"></a>Azure 的 Keyvault 功能：
- JDBC 驅動程式 6.0.0 
    - 相依性版本： Azure Keyvault （版本 0.9.7）、 Adal4j （版本 1.3.0），及其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))
- JDBC 驅動程式版本 6.2.2 和更新版本 （包括最新 6.4.0）
    - 相依性版本： Azure Keyvault （1.0.0 版）、 Adal4j （版本 1.4.0），及其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))

> [!NOTE]
>   為準，v6.2.2，azure-keyvault-java 相依性會更新以 1.0.0 版。 不過，新的版本與先前的版本 （版本 0.9.7） 不相容，因此驅動程式會中斷現有的實作。 驅動程式中的新實作需要依次中斷用戶端程式使用 Azure 金鑰保存庫功能的應用程式開發介面變更。

  
 ### <a name="azure-active-directory-authentication"></a>Azure Active Directory 驗證：
- JDBC 驅動程式 6.0.0 
    - 相依性版本： Adal4j （版本 1.3.0），以及其相依性
        - 在這個版本的驅動程式，您可以使用連線*ActiveDirectoryIntegrated*只能在 Windows 作業系統，並使用 SQL Server （sqljdbc_auth.dll 和 Active Directory Authentication Library 上的驗證模式ADALSQL。DLL)。 
- JDBC Driver version 6.4.0
    - 相依性版本： Adal4j （版本 1.4.0） 和其相依性
        - 在這個版本的驅動程式，您的應用程式不需要使用 ADALSQL。DLL。 根據作業系統中。 如**非 Windows 作業系統**，驅動程式需要使用 ActiveDirectoryIntegrated 驗證的 Kerberos 票證。 請參閱[Windows、 Linux 和 Mac 上的 設定 Kerberos 票證](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)如需詳細資訊。 如**Windows 作業系統**，預設的驅動程式會檢查 sqljdbc_auth.dll 是否已載入，而且不需要 Kerberos 票證安裝程式或 adal4j 相依性。 不過，如果未載入 sqljdbc_auth.dll，驅動程式的行為與非 Windows 作業系統相同的方式，並需要安裝程式，下列範例中所述： 使用這項功能的範例應用程式可以找到[這裡](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md).

 ## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式 GitHub 儲存機制](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 驅動程式 API 參考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  