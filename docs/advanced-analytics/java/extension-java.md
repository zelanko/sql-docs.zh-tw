---
title: 在 SQL Server 2019 的 Java 語言擴充功能 |Microsoft Docs
description: 使用 Java 語言擴充功能的 SQL Server 2019 上執行 Java 程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2d69a255c56c3b15051a393b74eb1492a4f830f4
ms.sourcegitcommit: 93e3bb8941411b808e00daa31121367e96fdfda1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49359335"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 的 Java 語言擴充功能 

從 SQL Server 2019 開始，您可以自訂的 Java 程式碼中執行[擴充性架構](../concepts/extensibility-framework.md)資料庫引擎執行個體的附加元件。 

擴充性架構，是執行外部程式碼的架構： Java （從 SQL Server 2019）， [（從 SQL Server 2017） 的 Python](../concepts/extension-python.md)，並[（從 SQL Server 2016） 的 R](../concepts/extension-r.md)。 執行程式碼是與核心引擎處理序隔離，但與 SQL Server 查詢執行完全整合。 這表示您可以將資料從任何 SQL Server 查詢推送至外部的執行階段，並取用或保存回 SQL Server 中的結果。

如同任何程式設計語言擴充功能，系統預存程序[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是執行預先編譯的 Java 程式碼的介面。

## <a name="prerequisites"></a>先決條件

需要 SQL Server 2019。 較早版本不需要 Java 整合。 

Java 版本需求是根據 Windows 和 Linux 而異。 Java Runtime Environment (JRE) 是最低需求，但 Jdk 適用於您需要的 Java 編譯器或開發套件。 因為 JDK 是全部 （含），如果您安裝 JDK、 JRE 不是必要的。

| 作業系統 | Java 版本 | JRE 下載 | JDK 下載 |
|------------------|--------------|--------------|--------------|
| Windows          | 1.10         | [JRE 10](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

在 Linux 上， **mssql 伺服器擴充性-java**套件會自動安裝 JRE 1.8，如果尚未安裝。 安裝指令碼也會新增至名為 JAVA_HOME 環境變數的 JVM 路徑。

在 Windows，建議您安裝的 JDK，在預設 /Program 檔案 / 資料夾的話。 否則，額外的設定，才能授與權限可執行檔。 如需詳細資訊，請參閱 <<c0> [ 授與權限 (Windows)](#perms-nonwindows)這份文件中的一節。

> [!Note]
> 提供 Java 是具有回溯相容性，舊版可能會運作，但資料表中列出的支援並經過測試的版本，這個早期的 CTP 版本。

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>在 Linux 上安裝

您可以安裝[資料庫引擎和 Java 延伸模組一起](../../linux/sql-server-linux-setup-machine-learning.md#chained-installation)，或將 Java 支援新增至現有的執行個體。 下列範例會將 Java 延伸模組新增至現有安裝。  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility-java
```

當您安裝**mssql 伺服器擴充性-java**，封裝會自動安裝 JRE 1.8，如果尚未安裝。 另外還會新增至名為 JAVA_HOME 環境變數的 JVM 路徑。

完成安裝之後下, 一個步驟是[設定外部指令碼執行](#configure-script-execution)。

> [!Note]
> 在連線網際網路的裝置，會下載套件相依性，並將其安裝主套件安裝過程中。 如需詳細資訊，包括離線安裝程式，請參閱[在 Linux 上安裝 SQL Server Machine Learning](../../linux/sql-server-linux-setup-machine-learning.md)。

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>在 Windows 上安裝

1. [執行安裝程式](../install/sql-machine-learning-services-windows-install.md)安裝 SQL Server 2019。

2. 當您前往 特徵選取時，請選擇**Machine Learning 服務 （資料庫）**。 

   雖然 Java 整合並未隨附於機器學習程式庫，這是提供擴充性架構的安裝程式中的選項。 如果您想要您可以省略 R 和 Python。

3. 完成安裝精靈，然後繼續進行下面兩個工作。

### <a name="add-the-javahome-variable"></a>將 JAVA_HOME 變數

JAVA_HOME 是環境變數，可指定 Java 解譯器的位置。 在此步驟中，為其在 Windows 上建立系統環境變數。

1. 尋找並複製/JRE 的 JDK 安裝路徑 (例如，C:\Program Files\Java\jdk-10.0.2)。

  在 CTP 2.0 中，將 JAVA_HOME 設定為基底的 jdk 資料夾僅適用於 Java 1.10。 

  適用於 Java 1.8，擴充到您 JDK (例如，"C:\Program Files\Java\jdk1.8.0_181\bin\server"在 Windows 上的 jvm.dll 路徑。 或者，您可以指向 JRE 的基底資料夾:"C:\Program Files\Java\jre1.8.0_181"。

2. 在控制台中，開啟**系統及安全性**，開啟**系統**，然後按一下**進階系統屬性**。

3. 按一下 **環境變數**。

4. 為 JAVA_HOME 中建立新的系統變數。

   ![環境變數中的 Java 首頁](../media/java/env-variable-java-home.png "設定適用於 Java")

<a name="perms-nonwindows"></a>

### <a name="grant-permissions-to-java-executables"></a>Java 可執行檔的權限授與

根據預設，外部處理序所執行的帳戶沒有存取 JRE 或 JDK 檔案。 在本節中，執行下列 PowerShell 指令碼，以允許存取的權限授與。

1. 尋找並複製 JDK 或 JRE 安裝位置。 比方說，它可能會是 C:\Program Files\Java\jdk-10.0.2。

2. 使用系統管理員權限開啟 PowerShell。 如果您不熟悉這項工作，請參閱[這篇文章](https://www.top-password.com/blog/5-ways-to-run-powershell-as-administrator-in-windows-10/)的提示。

3. 執行下列程式碼授與**SQLRUserGroup** Java 可執行檔的權限。 

  **SQLRUserGroup**指定下執行的外部處理序的權限。 根據預設，此群組的成員有權限的 R 和 Python 程式安裝 SQL Server，但不能在 Java 檔案。 若要執行 Java 可執行檔，您必須提供**SQLRUserGroup**執行這項操作的權限。

   ```powershell
   $Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
   $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
   $Acl.SetAccessRule($Ar)
   Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
   ```
4. 執行下列程式碼授與**ALL APPLICATION PACKAGES**以及權限。 

  在 SQL Server 2019，容器將做為隔離機制，背景工作帳戶與 Launchpad 服務帳戶，也就是成員的身分識別之下的容器內執行的程序**SQLRUserGroup**。 如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server 2019 差異](../install/sql-machine-learning-services-ver15.md)。

   ```powershell
   $Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
   $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
   $Acl.SetAccessRule($Ar) 
   Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
   ```

5. 重複前的兩個步驟，在包含您想要在 SQL Server 上執行的.class 或.jar 檔案的任何 Java classpath 資料夾。 例如，如果您在路徑，例如 C:\JavaPrograms\my-app 中編譯的程式，授與**SQLRUserGroup**並**ALL APPLICATION PACKAGES**資料夾的權限，讓程式可以載入。

  請務必授與權限的完整路徑，從根資料夾開始。 包含的資料夾的權限無法滿足載入您的程式碼。

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>設定指令碼執行

此時，就幾乎準備好要在 Linux 或 Windows 上執行 Java 程式碼。 最後一個步驟中，切換至 SQL Server Management Studio 或執行 TRANSACT-SQL 指令碼，以啟用外部指令碼執行的另一種工具。

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>確認安裝

若要確認安裝是否運作正常，請建立並執行[範例應用程式](java-first-sample.md)使用您剛安裝的 JDK，將這些檔案放在您稍早設定的 classpath 中。

## <a name="differences-in-ctp-20"></a>在 CTP 2.0 中的差異

如果您已熟悉使用機器學習服務，擴充功能的授權和隔離模型已變更在此版本中。 如需詳細資訊，請參閱 < [SQL Server 機器 2019 Learning Services 安裝中的差異](../install/sql-machine-learning-services-ver15.md)。

## <a name="limitations-in-ctp-20"></a>在 CTP 2.0 中的限制

* 輸入和輸出緩衝區中的值數目不能超過`MAX_INT (2^31-1)`因為這是可配置在 Java 中陣列的項目數目上限。

* 輸出中的參數[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)此版本中不支援。

* 在這個版本中的輸入和輸出資料集沒有 LOB 資料類型支援。 請參閱[Java 和 SQL Server 資料型別](java-sql-datatypes.md)的哪些資料類型支援此 CTP 中的詳細資料。

* 使用串流 sp_execute_external_script 參數@r_rowsPerRead此 CTP 中不支援。

* 資料分割使用 sp_execute_external_script 參數@input_data_1_partition_by_columns此 CTP 中不支援。

## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 範例](java-first-sample.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)