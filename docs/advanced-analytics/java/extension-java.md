---
title: 在 SQL Server 2019 的 Java 語言擴充功能 |Microsoft Docs
description: 使用 Java 語言擴充功能的 SQL Server 2019 上執行 Java 程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8acb0a72435306cdec8740ffb41ff499eea61fac
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714987"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 的 Java 語言擴充功能 

從 SQL Server 2019 開始，您可以自訂的 Java 程式碼中執行[擴充性架構](../concepts/extensibility-framework.md)資料庫引擎執行個體的附加元件。 

擴充性架構，是執行外部程式碼的架構： Java （從 SQL Server 2019）， [（從 SQL Server 2017） 的 Python](../concepts/extension-python.md)，並[（從 SQL Server 2016） 的 R](../concepts/extension-r.md)。 執行程式碼是與核心引擎處理序隔離，但與 SQL Server 查詢執行完全整合。 這表示您可以將資料從任何 SQL Server 查詢推送至外部的執行階段，並取用或保存回 SQL Server 中的結果。

如同任何程式設計語言擴充功能，系統預存程序[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是執行預先編譯的 Java 程式碼的介面。

## <a name="1---feature-installation"></a>1-功能安裝

若要安裝的 Java 語言擴充功能的 Windows 或 Linux 上執行 SQL Server 2019 安裝程式。 需要 SQL Server 2019 資料庫引擎執行個體。 您無法新增 Java 整合至較早版本。

在 Windows 中上, 啟動[安裝精靈](../install/sql-machine-learning-services-windows-install.md)。 在 特徵選取中選取**Machine Learning 服務 （資料庫）**。 雖然 Java 整合並未隨附於機器學習程式庫，這是提供擴充性架構的安裝程式中的選項。 如果您想要您可以省略 R 和 Python。

在 Linux 上，安裝[資料庫引擎](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)，並將[擴充性的套件和 Java 延伸套件](../../linux/sql-server-linux-setup-machine-learning.md)。

下列範例說明每個 Linux 作業系統的語法。

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility
sudo zypper install mssql-server-extensibility-java
```

## <a name="2---configuration"></a>2-設定

使用 SQL Server Management Studio 或執行 TRANSACT-SQL 指令碼的另一種工具，在 database engine 執行個體上設定外部指令碼執行。

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="3---bring-your-own-java"></a>3-攜帶您自己的 Java

從先前的語言整合，例如 R 和 Python 的一項差異是，您可以控制與 SQL Server 搭配使用 JVM。

| Java 版本 | 作業系統 |
|--------------|------------------|
| [Java 1.10](http://jdk.java.net/10/)   | Windows |
| Java 1.8   | Linux | 

提供 Java 是具有回溯相容性，舊版可能會運作，但資料表中列出的支援並經過測試的版本，這個早期的 CTP 版本。

> [!Note]
>若要使用 SQL Server 中執行 Java，您就技術上而言只需要[Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html)安裝 (JRE)。 JDK 是開發套件，包括 Java 編譯器和其他開發相關的封裝。 如果您已經擁有開發環境，只需要在伺服器電腦上的 Java 執行階段，您可以略過的 JDK 安裝指示，並只安裝 JRE。

## <a name="jdk-on-windows"></a>在 Windows 上的 JDK

下載 Windows 版[Java SE Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)。

安裝的 JDK，在預設 /Program 檔案 / 資料夾，如果您想要避免授與讀取權限**ALL APPLICATION PACKAGES**並**SQLRUserGroup**替代位置上的安全性群組. 您的 Java classpath 資料夾，其中保存.class 或.jar 檔案存取適用於相同的指引。 

> [!Note]
> 擴充功能的授權和隔離模型已在此版本中變更。 如需詳細資訊，請參閱 < [SQL Server 機器 2019 Learning Services 安裝中的差異](../install/sql-machine-learning-services-ver15.md)。

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>授與存取非預設 JDK 資料夾 (僅 Windows)

如果您安裝 JDK/JRE 的預設資料夾中，您可以略過此步驟。 針對非預設資料夾安裝，執行下列 PowerShell 指令碼，授與存取權**SQLRUsergroup**和 SQL Server 服務帳戶 （在 ALL_APPLICATION_PACKAGES) 來存取 JVM 和 Java 類別路徑。

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup 權限

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
$Acl.SetAccessRule($Ar)
Set-Acl ""<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

#### <a name="appcontainer-permissions"></a>AppContainer 權限

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
$Acl.SetAccessRule($Ar) 
Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

### <a name="add-the-jdk-path-to-javahome"></a>將 JDK 路徑新增至 JAVA_HOME
您也需要將 JDK/JRE 安裝路徑 (例如，"C:\Program Files\Java\jdk-10.0.2") 新增至系統環境變數您命名 「 JAVA_HOME"。 

若要建立的系統變數，使用 [控制台] > 系統及安全性 > 系統來存取**進階系統屬性**。 按一下 **環境變數**JAVA_HOME 然後建立新的系統變數。

![環境變數中的 Java 首頁](../media/java/env-variable-java-home.png "設定適用於 Java")

## <a name="jdk-on-linux"></a>在 Linux 上的 JDK

在 Linux 上的 mssql 伺服器擴充性-java 套件會自動安裝 JRE 1.8 如果尚未安裝。 另外還會新增至名為 JAVA_HOME 環境變數的 JVM 路徑。

## <a name="limitations-in-ctp-20"></a>在 CTP 2.0 中的限制

* 輸入和輸出緩衝區中的值數目不能超過`MAX_INT (2^31-1)`因為這是可配置在 Java 中陣列的項目數目上限。

* 在此版本不支援 sp_execute_external_script 中的輸出參數。

* 在這個版本中的輸入和輸出資料集沒有 LOB 資料類型支援。 請參閱[Java 和 SQL Server 資料型別](java-sql-datatypes.md)的哪些資料類型支援此 CTP 中的詳細資料。

* 使用串流 sp_execute_external_script 參數@r_rowsPerRead此 CTP 中不支援。

* 資料分割使用 sp_execute_external_script 參數@input_data_1_partition_by_columns此 CTP 中不支援。

## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 範例](java-first-sample.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)