---
title: JDBC 驅動程式的系統需求 | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a6aac999ef6877356f66f4db1d6d6763cc0f1ea
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903725"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 驅動程式的系統需求
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 的資料，您的電腦上必須安裝下列元件：

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([下載](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment 需求  

 自 Microsoft JDBC Driver 8.2 for SQL Server 起開始支援 Java 開發套件 (JDK) 13.0 及 Java Runtime Environment (JRE) 13.0。

 自 Microsoft JDBC Driver 7.4 for SQL Server 起開始支援 Java 開發套件 (JDK) 12.0 及 Java Runtime Environment (JRE) 12.0。

 自 Microsoft JDBC Driver 7.2 for SQL Server 起開始支援 Java 開發套件 (JDK) 11.0 及 Java Runtime Environment (JRE) 11.0。
 
 自 Microsoft JDBC Driver 7.0 for SQL Server 起開始支援 Java 開發套件 (JDK) 10.0 及 Java Runtime Environment (JRE) 10.0。

 自 Microsoft JDBC Driver 6.4 for SQL Server 起開始支援 Java 開發套件 (JDK) 9.0 及 Java Runtime Environment (JRE) 9.0。

 自 Microsoft JDBC Driver 4.2 for SQL Server 起開始支援 Java 開發套件 (JDK) 8.0 及 Java Runtime Environment (JRE) 8.0。 Java 資料庫連線 (JDBC) Spec API 支援已經過擴充，可包含 JDBC 4.1 和 4.2 API。
  
 自 Microsoft JDBC Driver 4.1 for SQL Server 起開始支援 Java 開發套件 (JDK) 7.0 及 Java Runtime Environment (JRE) 7.0。
  
 從 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 開始，JDBC 驅動程式的 Java Database Connectivity (JDBC) Spec API 支援已經過擴充，可包含 JDBC 4.0 API。 Sun Java SE 開發套件 (JDK) 6.0 及 Java Runtime Environment (JRE) 6.0 同時引進了 JDBC 4.0 API。 JDBC 4.0 是 JDBC 3.0 API 的超集。
  
 當您在 Windows 及 UNIX 作業系統上部署 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，必須分別使用安裝套件 *sqljdbc_\<版本>_enu.exe* 及 *sqljdbc_\<版本>_enu.tar.gz*。 如需如何部署 JDBC 驅動程式的詳細資訊，請參閱[部署 JDBC 驅動程式](../../connect/jdbc/deploying-the-jdbc-driver.md)主題。  

**Microsoft JDBC Driver 8.2 for SQL Server：**  

  JDBC Driver 8.2 在每個安裝套件中均包含三個 JAR 類別庫：**mssql-jdbc-8.2.1.jre8.jar**、**mssql-jdbc-8.2.1.jre11.jar** 和 **mssql-jdbc-8.2.1.jre13.jar**。

  JDBC Driver 8.2 專為搭配所有主要 Java 虛擬機器運作而設計，且所有 Java 虛擬機器皆能支援，但只在 OpenJDK 1.8、OpenJDK 11.0、OpenJDK 13.0、Azul Zulu JRE 1.8、Azul Zulu JRE 11.0 與 Azul Zulu JRE 13.0 上測試過。
  
  以下摘要說明 Microsoft JDBC Drivers 8.2 for SQL Server 所隨附這兩個 JAR 檔案提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-8.2.1.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 1.8。 使用 JRE 1.7 或更舊版本會擲回例外狀況。<br /><br /> 8\.2 中的新功能包括：JDK 13 支援、具有安全記憶體保護區的 Always Encrypted，以及時態性資料類型效能改善。 |
|mssql-jdbc-8.2.1.jre11.jar|4.3|11|需要 Java Runtime Environment (JRE) 11.0。 使用 JRE 10.0 或更舊版本會擲回例外狀況。<br /><br /> 8\.2 中的新功能包括：JDK 13 支援、具有安全記憶體保護區的 Always Encrypted，以及時態性資料類型效能改善。 |
|mssql-jdbc-8.2.1.jre13.jar|4.3|13|需要 Java Runtime Environment (JRE) 13.0。 使用 JRE 11.0 或更舊版本會擲回例外狀況。<br /><br /> 8\.2 中的新功能包括：JDK 13 支援、具有安全記憶體保護區的 Always Encrypted，以及時態性資料類型效能改善。 |


  JDBC Driver 8.2 也可在 Maven 中央存放庫上取得，且可藉由在 POM.XML 中新增下列程式碼來新增至 Maven 專案：  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.2.1.jre11</version>
</dependency>
```

**Microsoft JDBC Driver 7.4 for SQL Server：**  

  JDBC Driver 7.4 在每個安裝套件中包含三個 JAR 類別庫：**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar** 和 **mssql-jdbc-7.4.1.jre12.jar**。

  JDBC Driver 7.4 專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但只在 OpenJDK 1.8、OpenJDK 11.0、OpenJDK 12.0、Azul Zulu JRE 1.8、Azul Zulu JRE 11.0 與 Azul Zulu JRE 12.0 上測試過。
  
  以下摘要說明 Microsoft JDBC Drivers 7.4 for SQL Server 隨附這兩個 JAR 檔案所提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.4.1.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 1.8。 使用 JRE 1.7 或更舊版本會擲回例外狀況。<br /><br /> 7\.4 中的新功能包括：JDK 12 支援、NTLM 驗證及 useFmtOnly。 |    
|mssql-jdbc-7.4.1.jre11.jar|4.3|11|需要 Java Runtime Environment (JRE) 11.0。 使用 JRE 10.0 或更舊版本會擲回例外狀況。<br /><br /> 7\.4 中的新功能包括：JDK 12 支援、NTLM 驗證及 useFmtOnly。 |  
|mssql-jdbc-7.4.1.jre12.jar|4.3|12|需要 Java Runtime Environment (JRE) 12.0。 使用 JRE 11.0 或更舊版本會擲回例外狀況。<br /><br /> 7\.4 中的新功能包括：JDK 12 支援、NTLM 驗證及 useFmtOnly。 |   


  JDBC Driver 7.4 也可在 Maven 中央存放庫上取得，而且可經由在 POM.XML 中新增下列程式碼，新增到 Maven 專案：  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```

**Microsoft JDBC Driver 7.2 for SQL Server：**  

  JDBC Driver 7.2 會在每個安裝套件中包括兩個 JAR 類別庫：**mssql-jdbc-7.2.2.jre8.jar** 與 **mssql-jdbc-7.2.2.jre11.jar**。

  JDBC Driver 7.2 專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但此驅動程式只在 OpenJDK 8.0、OpenJDK 11.0、Azul Zulu JRE 8.0 與 Azul Zulu JRE 11.0 上測試過。
  
  下列摘要說明 Microsoft JDBC Drivers 7.2 for SQL Server 隨附的這兩個 JAR 檔案所提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.2.2.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更舊版本會擲回例外狀況。<br /><br /> 7\.2 中的新功能包括：JDK 11 支援、Active Directory 受控服務識別 (MSI) 驗證、OSGi 支援、SQLServerError API。 |    
|mssql-jdbc-7.2.2.jre11.jar|4.3|10|需要 Java Runtime Environment (JRE) 11.0。 使用 JRE 10.0 或更舊版本會擲回例外狀況。<br /><br /> 7\.2 中的新功能包括：JDK 11 支援、Active Directory 受控服務識別 (MSI) 驗證、OSGi 支援、SQLServerError API。 |    


  JDBC Driver 7.2 也可在 Maven 中央存放庫上取得，而且可在 POM.XML 中新增下列程式碼，藉以新增至 Maven 專案：  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
</dependency>
```
 
**Microsoft JDBC Driver 7.0 for SQL Server：**  

  JDBC Driver 7.0 在每個安裝套件中包含兩個 JAR 類別庫：**mssql-jdbc-7.0.0.jre8.jar** 和 **mssql-jdbc-7.0.0.jre10.jar**。

  JDBC Driver 7.0 專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但此驅動程式只經過 OpenJDK 8.0 及 10.0 的測試。
  
  下列摘要說明隨附於 Microsoft JDBC Drivers 7.0 for SQL Server 的兩個 JAR 檔案所提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更舊版本會擲回例外狀況。<br /><br /> 7\.0 中的新功能包括：JDK 10 支援、將預設的合規性層級更新為 JDBC 4.2 規格、空間資料類型支援、cancelQueryTimeout 連線屬性、要求界限方法、useBulkCopyForBatchInsert 連線屬性、資料探索與分類資訊、UTF-8 功能擴充，以及 CityHash 支援。 |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|需要 Java Runtime Environment (JRE) 10.0。 使用 JRE 9.0 或更舊版本會擲回例外狀況。<br /><br /> 7\.0 中的新功能包括：JDK 10 支援、將預設的合規性層級更新為 JDBC 4.2 規格、空間資料類型支援、cancelQueryTimeout 連線屬性、要求界限方法、useBulkCopyForBatchInsert 連線屬性、資料探索與分類資訊、UTF-8 功能擴充，以及 CityHash 支援。 |    


  JDBC Driver 7.0 也可在 Maven 中央存放庫上取得，而且可在 POM.XML 中新增下列程式碼，藉以新增至 Maven 專案：  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```
  
**Microsoft JDBC Driver 6.4 for SQL Server：**  

  JDBC Driver 6.4 在每個安裝套件中包含三個 JAR 類別庫：**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar** 和 **mssql-jdbc-6.4.0.jre9.jar**。

  JDBC Driver 6.4 專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但此驅動程式只經過 OpenJDK 7.0、8.0 及 9.0 的測試。
  
  下列摘要說明隨附於 Microsoft JDBC Drivers 6.4 for SQL Server 的三個 JAR 檔案所提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.4 中的新功能包括：適用於 Linux 的 Azure AD 驗證、適用於 Kerberos 的主體/密碼方法、在 SPN 中自動偵測領域以進行跨網域驗證、Kerberos 限制委派、查詢逾時、通訊端逾時，以及重複使用備妥的陳述式控制代碼。 |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.4 中的新功能包括：適用於 Linux 的 Azure AD 驗證、適用於 Kerberos 的主體/密碼方法、在 SPN 中自動偵測領域以進行跨網域驗證、Kerberos 限制委派、查詢逾時、通訊端逾時，以及重複使用備妥的陳述式控制代碼。 |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|需要 Java Runtime Environment (JRE) 9.0。 使用 JRE 8.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.4 中的新功能包括：適用於 Linux 的 Azure AD 驗證、適用於 Kerberos 的主體/密碼方法、在 SPN 中自動偵測領域以進行跨網域驗證、Kerberos 限制委派、查詢逾時、通訊端逾時，以及重複使用備妥的陳述式控制代碼。 |

JDBC Driver 6.4 也可在 Maven 中央存放庫上取得，而且可在 POM.XML 中新增下列程式碼，藉以新增至 Maven 專案： 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 for SQL Server：**  
  
  JDBC Driver 6.2 在每個安裝套件中包含兩個 JAR 類別庫：**mssql-jdbc-6.2.2.jre7.jar** 和 **mssql-jdbc-6.2.2.jre8.jar**。 
  
 JDBC Driver 6.2 專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但此驅動程式只經過 Sun JRE 5.0、6.0、7.0 及 8.0 的測試。
  
 下列摘要說明隨附於 Microsoft JDBC Drivers 6.0 與 4.2 for SQL Server 的三個 JAR 檔案所提供的支援：  
  
|JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-jdbc-6.2.2.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.2 中的新功能包括：適用於 Linux 的 Azure AD 驗證、適用於 Kerberos 的主體/密碼方法、在 SPN 中自動偵測領域以進行跨網域驗證、Kerberos 限制委派、查詢逾時、通訊端逾時，以及重複使用備妥的陳述式控制代碼。 |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.2 中的新功能包括：適用於 Linux 的 Azure AD 驗證、適用於 Kerberos 的主體/密碼方法、在 SPN 中自動偵測領域以進行跨網域驗證、Kerberos 限制委派、查詢逾時、通訊端逾時，以及重複使用備妥的陳述式控制代碼。|    

  JDBC Driver 6.2 也可在 Maven 中央存放庫上取得，而且可在 POM.XML 中新增下列程式碼，藉以新增至 Maven 專案： 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 與 4.2 for SQL Server：**  
  
  JDBC Drivers 6.0 和 4.2 會在每個安裝套件中包括兩個 JAR 類別庫：**sqljdbc41.jar** 和 **sqljdbc42.jar**。 
  
 JDBC Driver 6.0 與 4.2 專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但這兩個驅動程式只經過 Sun JRE 5.0、6.0、7.0 及 8.0 的測試。
  
 下列摘要說明隨附於 Microsoft JDBC Drivers 6.0 與 4.2 for SQL Server 的三個 JAR 檔案所提供的支援：  
  
|JAR|JDBC 版本相容性|建議的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.0 與 4.2 套件中的新功能包括：JDBC 4.1 合規性和大量複製<br /><br /> 此外，僅包含在 6.0 套件中的新功能包括：Always Encrypted、資料表值參數、Azure Active Directory 驗證、以透明方式連線至 Always On 可用性群組、改進針對備妥查詢和國際化網域名稱 (IDN) 所擷取的參數中繼資料|  
|sqljdbc42.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更舊版本會擲回例外狀況。<br /><br /> 6\.0 與 4.2 套件中的新功能包括：JDBC 4.1 合規性、JDBC 4.2 合規性及大量複製<br /><br /> 此外，僅包含在 6.0 套件中的新功能包括：Always Encrypted、資料表值參數、Azure Active Directory 驗證、以透明方式連線至 Always On 可用性群組、改進針對備妥查詢和國際化網域名稱 (IDN) 所擷取的參數中繼資料|  
  
 **Microsoft JDBC Driver 4.1 for SQL Server：**  
  
 JDBC Driver 4.1 會在每個安裝套件中包括一個 JAR 類別庫：**sqljdbc41.jar**。  
    
|JAR|描述|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** 類別庫會提供 JDBC 4.0 API 的支援。 它包含 JDBC 4.0 驅動程式的所有功能，以及 JDBC 4.0 API 方法。 不支援 JDBC 4.1 (會擲回例外狀況 "SQLFeatureNotSupportedException")。<br /><br /> **sqljdbc41.jar** 類別庫需要使用 Java Runtime Environment (JRE) 7.0。 在 JRE 6.0 與 5.0 上使用 **sqljdbc41.jar** 就會擲回例外狀況。<br /><br /> 
  
 JDBC 驅動程式專為搭配所有主要 Java 虛擬機器運作而設計，而且所有 Java 虛擬機器皆能支援，但此驅動程式只經過 Sun JRE 5.0、6.0 及 7.0 的測試。
  
 下列摘要說明隨附於 Microsoft JDBC Drivers 4.1 for SQL Server 的 JAR 檔案所提供的支援。  
  
|JAR|JDBC 版本|JRE (可以執行)|JDK (可以編譯)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 需求  
 JDBC 驅動程式支援與 Azure SQL 資料庫及 SQL Server 的連線。 從 SQL Server 2008 開始支援 Microsoft JDBC Driver 4.2 與 4.1 for SQL Server。
  
## <a name="operating-system-requirements"></a>作業系統需求  
 JDBC Driver 設計為可以在支援使用 JAVA 虛擬機器 (JVM) 的任何作業系統上運作。 不過，僅在 Sun Solaris、SUSE Linux、Ubuntu Linux、CentOS Linux、macOS 及 Windows 作業系統上正式測試過。  
  
## <a name="supported-languages"></a>支援的語言  
 JDBC 驅動程式支援所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行定序。 如需有關 JDBC 驅動程式所支援的定序詳細資訊，請參閱 [JDBC 驅動程式的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)。  
  
 如需定序的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書中的＜使用定序＞。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
