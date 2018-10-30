---
title: JDBC 驅動程式的系統需求 |Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2ddf8f5c03d6f4c6724075e7209d800e10f7e39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724296"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 驅動程式的系統需求
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 的資料，您的電腦上必須安裝下列元件：

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([下載](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment 需求  
 從 Microsoft JDBC Driver 7.0 for SQL Server 開始，支援 Sun Java SE 開發套件 (JDK) 10.0 與 Java Runtime Environment (JRE) 10.0。

 從 Microsoft JDBC Driver 6.4 for SQL Server 開始，支援 Sun Java SE 開發套件 (JDK) 9.0 與 Java Runtime Environment (JRE) 9.0。

 從 Microsoft JDBC Driver 4.2 for SQL Server 開始支援 Sun Java SE 開發套件 (JDK) 8.0 與 Java Runtime Environment (JRE) 8.0。 Java 資料庫連線 (JDBC) Spec API 支援已經過擴充，可包含 JDBC 4.1 和 4.2 API。  
  
 從 Microsoft JDBC Driver 4.1 for SQL Server 開始支援 Sun Java SE 開發套件 (JDK) 7.0 與 Java Runtime Environment (JRE) 7.0。  
  
 從 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 開始，JDBC 驅動程式的 Java Database Connectivity (JDBC) Spec API 支援已經過擴充，可包含 JDBC 4.0 API。 JDBC 4.0 API 導入成 Sun Java SE Development Kit (JDK) 6.0 和 Java Runtime Environment (JRE) 6.0 的一部分。 JDBC 4.0 是 JDBC 3.0 API 的超集。  
  
 當您在 Windows 及 UNIX 作業系統上部署 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，必須分別使用安裝套件 *sqljdbc_\<版本>_enu.exe* 及 *sqljdbc_\<版本>_enu.tar.gz*。 如需如何部署 JDBC 驅動程式的詳細資訊，請參閱[部署 JDBC Driver](../../connect/jdbc/deploying-the-jdbc-driver.md)主題。  
  
**Microsoft JDBC Driver 7.0 for SQL Server：**  

  JDBC Driver 7.0 在每個安裝套件中包含兩個 JAR 類別庫：**mssql-jdbc-7.0.0.jre8.jar** 和 **mssql-jdbc-7.0.0.jre10.jar**。

  JDBC 驅動程式 7.0 是設計用來與所有主要 Sun 對應的 Java 虛擬機器搭配使用並受其支援，但僅在 Sun JRE 8.0 與 10.0 上測試過。
  
  下列摘要說明隨附於 Microsoft JDBC Drivers 7.0 for SQL Server 的兩個 JAR 檔案所提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或較低的擲回例外狀況。<br /><br /> 在 7.0 中的新功能包括： JDK 10 支援、 JDBC 4.2 規格、 空間資料類型支援、 cancelQueryTimeout 連接屬性、 界限要求方法、 useBulkCopyForBatchInsert 連接屬性，資料更新的預設相容性層級探索與分類的資訊、 utf-8 功能延伸模組和 CityHash 支援。 |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|需要 Java Runtime Environment (JRE) 10.0。 使用 JRE 9.0 或較低的擲回例外狀況。<br /><br /> 在 7.0 中的新功能包括： JDK 10 支援、 JDBC 4.2 規格、 空間資料類型支援、 cancelQueryTimeout 連接屬性、 界限要求方法、 useBulkCopyForBatchInsert 連接屬性，資料更新的預設相容性層級探索與分類的資訊、 utf-8 功能延伸模組和 CityHash 支援。 |    


  JDBC 驅動程式 7.0 也會提供在 Maven 中央儲存機制，並可以 POM 中加入下列程式碼新增至 Maven 專案。XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```      
  
**Microsoft JDBC Driver 6.4 for SQL Server：**  

  JDBC Driver 6.4 在每個安裝套件中包含三個 JAR 類別庫：**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar** 和 **mssql-jdbc-6.4.0.jre9.jar**。

  JDBC 驅動程式 6.4 是設計用來與所有主要 Sun 對應的 Java 虛擬機器搭配使用並受其支援，但僅在 Sun JRE 7.0、8.0 與 9.0 上測試過。
  
  下列摘要說明隨附於 Microsoft JDBC Drivers 6.4 for SQL Server 的三個 JAR 檔案所提供的支援：  
  
  |JAR|JDBC 版本相容性|建議的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或較低的擲回例外狀況。<br /><br /> 6.4 中的新功能包括： 適用於 Linux，主體/密碼方法 kerberos SPN 中的 REALM 自動偵測跨網域驗證，Kerberos 限制委派、 查詢逾時、 通訊端逾時，Azure AD 驗證和已備妥陳述式控制代碼重複使用。 |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或較低的擲回例外狀況。<br /><br /> 6.4 中的新功能包括： 適用於 Linux，主體/密碼方法 kerberos SPN 中的 REALM 自動偵測跨網域驗證，Kerberos 限制委派、 查詢逾時、 通訊端逾時，Azure AD 驗證和已備妥陳述式控制代碼重複使用。 |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|需要 Java Runtime Environment (JRE) 9.0。 使用 JRE 8.0 或較低的擲回例外狀況。<br /><br /> 6.4 中的新功能包括： 適用於 Linux，主體/密碼方法 kerberos SPN 中的 REALM 自動偵測跨網域驗證，Kerberos 限制委派、 查詢逾時、 通訊端逾時，Azure AD 驗證和已備妥陳述式控制代碼重複使用。 |

JDBC Driver 6.4 Maven 中央儲存機制位於也可用，且可以 POM 中加入下列程式碼新增至 Maven 專案。XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 for SQL Server：**  
  
  JDBC Driver 6.2 在每個安裝套件中包含兩個 JAR 類別庫：**mssql-jdbc-6.2.2.jre7.jar** 和 **mssql-jdbc-6.2.2.jre8.jar**。 
  
 JDBC 驅動程式 6.2 是設計用來與所有主要 Sun 對應的 Java 虛擬機器搭配使用並受其支援，但僅在 Sun JRE 5.0、6.0、7.0 與 8.0 上測試過。
  
 下列摘要說明隨附於 Microsoft JDBC Drivers 6.0 與 4.2 for SQL Server 的三個 JAR 檔案所提供的支援：  
  
|JAR|JDBC 版本相容性|建議的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-6.2.2.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或較低的擲回例外狀況。<br /><br /> 6.2 中的新功能包括： 適用於 Linux，主體/密碼方法 kerberos SPN 中的 REALM 自動偵測跨網域驗證，Kerberos 限制委派、 查詢逾時、 通訊端逾時，Azure AD 驗證和已備妥陳述式控制代碼重複使用。 |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或較低的擲回例外狀況。<br /><br /> 6.2 中的新功能包括： 適用於 Linux，主體/密碼方法 kerberos SPN 中的 REALM 自動偵測跨網域驗證，Kerberos 限制委派、 查詢逾時、 通訊端逾時，Azure AD 驗證和已備妥陳述式控制代碼重複使用|    

  JDBC Driver 6.2 Maven 中央儲存機制位於也可用，且可以 POM 中加入下列程式碼新增至 Maven 專案。XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 與 4.2 for SQL Server：**  
  
  JDBC 驅動程式 6.0 與 4.2 中每個安裝套件中包含兩個 JAR 類別庫： **sqljdbc41.jar**，並**sqljdbc42.jar**。 
  
 JDBC 驅動程式 6.0 與 4.2 是設計用來與所有主要 Sun 對應的 Java 虛擬機器搭配使用並受其支援，但僅在 Sun JRE 5.0、6.0、7.0 與 8.0 上測試過。 
  
 下列摘要說明隨附於 Microsoft JDBC Drivers 6.0 與 4.2 for SQL Server 的三個 JAR 檔案所提供的支援：  
  
|JAR|JDBC 版本相容性|建議的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或較低的擲回例外狀況。<br /><br /> 6.0 與 4.2 套件中的新功能包括：JDBC 4.1 相容性與大量複製<br /><br /> 此外，包含 6.0 套件中的新功能： Always Encrypted，資料表值參數，Azure Active Directory 驗證，Always On 可用性群組，針對擷取參數中繼資料中的改進的透明連接備妥查詢和國際化網域名稱 (IDN)|  
|sqljdbc42.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或較低的擲回例外狀況。<br /><br /> 6.0 與 4.2 套件中的新功能包括：JDBC 4.1 相容性、JDBC 4.2 相容性以及大量複製<br /><br /> 此外，包含 6.0 套件中的新功能： Always Encrypted，資料表值參數，Azure Active Directory 驗證，Always On 可用性群組，針對擷取參數中繼資料中的改進的透明連接備妥查詢和國際化網域名稱 (IDN)|  
  
 **Microsoft JDBC Driver 4.1 for SQL Server：**  
  
 JDBC Driver 4.1 中每個安裝套件包含一個 JAR 類別庫： **sqljdbc41.jar**。  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** 類別庫會提供 JDBC 4.0 API 的支援。 它包含 JDBC 4.0 驅動程式的所有功能，以及 JDBC 4.0 API 方法。 不支援 JDBC 4.1 (將會擲回例外狀況 "SQLFeatureNotSupportedException")。<br /><br /> **sqljdbc41.jar** 類別庫需要使用 Java Runtime Environment (JRE) 7.0。 使用**sqljdbc41.jar**在 JRE 6.0 與 5.0 上就會擲回例外狀況。<br /><br /> 
  
 JDBC 驅動程式是設計用來與所有主要 Sun 對應的 Java 虛擬機器搭配使用並受其支援，但已在 Sun JRE 5.0、6.0 與 7.0 上測試過。  
  
 下列摘要說明隨附於 Microsoft JDBC Drivers 4.1 for SQL Server 的 JAR 檔案所提供的支援。  
  
|JAR|JDBC 版本|JRE (可以執行)|JDK (可以編譯)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 需求  
 JDBC 驅動程式支援與 Azure SQL 資料庫及 SQL Server 的連線。 從 SQL Server 2008 開始支援 Microsoft JDBC Driver 4.2 與 4.1 for SQL Server。
  
## <a name="operating-system-requirements"></a>作業系統需求  
 JDBC Driver 設計為可以在支援使用 JAVA 虛擬機器 (JVM) 的任何作業系統上運作。 不過，僅在 Sun Solaris、SUSE Linux 及 Windows 作業系統上正式測試過。  
  
## <a name="supported-languages"></a>支援的語言  
 JDBC 驅動程式支援所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行定序。 如需有關 JDBC 驅動程式支援的定序的詳細資訊，請參閱 < [JDBC Driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)。  
  
 如需定序的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書中的＜使用定序＞。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
