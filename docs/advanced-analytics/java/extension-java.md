---
title: 在 SQL Server 2019-SQL Server Machine Learning 服務的 Java 語言擴充功能
description: 安裝、 設定及驗證的 Java 語言擴充功能於 SQL Server 2019 適用於 Linux 和 Windows 系統。
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a18886ea4daff3fb87853a556b67ad0562c2efd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017834"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 的 Java 語言擴充功能 

從 Windows 和 Linux 上的 SQL Server 2019 預覽中，您可以自訂的 Java 程式碼中執行[擴充性架構](../concepts/extensibility-framework.md)資料庫引擎執行個體的附加元件。 

擴充性架構是執行外部程式碼的架構：（從 SQL Server 2019，） 的 Java [（從 SQL Server 2017） 的 Python](../concepts/extension-python.md)，並[（從 SQL Server 2016） 的 R](../concepts/extension-r.md)。 執行程式碼是與核心引擎處理序隔離，但與 SQL Server 查詢執行完全整合。 這表示您可以將資料從任何 SQL Server 查詢推送至外部的執行階段，並取用或保存回 SQL Server 中的結果。

如同任何程式設計語言擴充功能，系統預存程序[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是執行預先編譯的 Java 程式碼的介面。

<a name="prerequisites"></a>

## <a name="prerequisites"></a>先決條件

需要 SQL Server 2019 預覽執行個體。 較早版本不需要 Java 整合。

支援 Java 8。 Java Runtime Environment (JRE) 是最低需求，但 Jdk 適用於您需要的 Java 編譯器或開發套件。 因為 JDK 是全部 （含），如果您安裝 JDK、 JRE 不是必要的。

您可以使用您慣用的 Java 8 散發套件。 以下是兩個建議的散發套件：

| Distribution | Java 版本 | 作業系統 | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows 和 Linux | 是 | 是 |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows 和 Linux | 是 | 否 |

在 Linux 上， **mssql 伺服器擴充性-java**套件會自動安裝 JRE 8，如果尚未安裝。 安裝指令碼也會新增至名為 JAVA_HOME 環境變數的 JVM 路徑。

在 Windows，建議您安裝在預設 JDK`/Program Files/`資料夾的話。 否則，額外的設定，才能授與權限可執行檔。 如需詳細資訊，請參閱 <<c0> [ 授與權限 (Windows)](#perms-nonwindows)這份文件中的一節。

> [!Note]
> 提供 Java 是具有回溯相容性，可更早版本，但這個早期的 CTP 版本的支援並經過測試的版本是 Java 8。 

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>在 Linux 上安裝

您可以安裝[資料庫引擎和 Java 延伸模組一起](../../linux/sql-server-linux-setup-machine-learning.md#install-all)，或將 Java 支援新增至現有的執行個體。 下列範例會將 Java 延伸模組新增至現有安裝。  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# SUSE install commands
sudo zypper install mssql-server-extensibility-java
```

當您安裝**mssql 伺服器擴充性-java**，封裝會自動安裝 JRE 8，如果尚未安裝。 另外還會新增至名為 JAVA_HOME 環境變數的 JVM 路徑。

完成安裝之後下, 一個步驟是[設定外部指令碼執行](#configure-script-execution)。

> [!Note]
> 在連線網際網路的裝置，會下載套件相依性，並將其安裝主套件安裝過程中。 如需詳細資訊，包括離線安裝程式，請參閱[在 Linux 上安裝 SQL Server Machine Learning](../../linux/sql-server-linux-setup-machine-learning.md)。

### <a name="grant-permissions-on-linux"></a>在 Linux 上的 授與權限

若要提供 SQL Server 權限才能執行 Java 類別，您需要設定權限。

若要授與讀取及執行 jar 檔案或類別檔案的存取權，請執行下列**chmod**命令在每一個類別或 jar 檔案。 我們建議您將類別檔案放在 jar 中，當您使用 SQL Server。 如需建立 jar 的說明，請參閱[如何建立的 jar 檔案](#create-jar)。

```cmd
chmod ug+rx <MyJarFile.jar>
```
您也需要授與目錄或 jar 檔案，以進行讀取/執行的 mssql_satellite 權限。

* 如果您從 SQL Server 呼叫類別檔案，mssql_satellite 會需要讀取/執行權限*每個*在資料夾階層中，從根目錄下的直接父目錄。

* 如果您從 SQL Server 呼叫 jar 檔案，就足以 jar 檔案本身上執行命令。

```cmd
chown mssql_satellite:mssql_satellite <directory>
```

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>在 Windows 上安裝

1. 確定已安裝支援的 Java 版本。 如需詳細資訊，請參閱 <<c0> [ 必要條件](#prerequisites)。

2. [執行安裝程式](../install/sql-machine-learning-services-windows-install.md)安裝 SQL Server 2019。

3. 當您前往 特徵選取時，請選擇**Machine Learning 服務 （資料庫）**。 

   雖然 Java 整合並未隨附於機器學習程式庫，這是提供擴充性架構的安裝程式中的選項。 如果您想要您可以省略 R 和 Python。

4. 完成安裝精靈，然後繼續進行下面兩個工作。

### <a name="add-the-javahome-variable"></a>將 JAVA_HOME 變數

JAVA_HOME 是環境變數，可指定 Java 解譯器的位置。 在此步驟中，為其在 Windows 上建立系統環境變數。

1. 尋找並複製 JDK/JRE 路徑 (例如`C:\Program Files\Java\jdk1.8.0_201`)。

    根據您慣用的 Java 散發套件，您的 JRE 的 JDK 的位置可能不同於上述的範例路徑。

2. 在控制台中，開啟**系統及安全性**，開啟**系統**，然後按一下**進階系統屬性**。

3. 按一下 **環境變數**。

4. 建立新的系統變數`JAVA_HOME`JDK/JRE 路徑 （在步驟 1 中找到） 的值。

5. 重新啟動[Launchpad](../concepts/extensibility-framework.md#launchpad)。

    1. 開啟 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。

    2. 在 SQL Server 服務，以滑鼠右鍵按一下 SQL Server 啟動控制板，然後選取**重新啟動**。

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>授與存取非預設 JDK 資料夾 (僅 Windows)

如果您安裝 JDK/JRE 的預設資料夾中，您可以略過此步驟。 

針對非預設資料夾安裝，執行**icacls**命令*提升權限*授與存取權的列**SQLRUsergroup**和 SQL Server 服務帳戶 （在**ALL_APPLICATION_PACKAGES**) 來存取 JVM 和 Java 類別路徑。 命令會以遞迴方式存取權授與所有檔案和資料夾下的指定的目錄路徑。

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup 權限

具名的執行個體中，執行個體名稱附加至 SQLRUsergroup (比方說， `SQLRUsergroupINSTANCENAME`)。

```cmd
icacls "<PATH TO CLASS or JAR FILES>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

#### <a name="appcontainer-permissions"></a>AppContainer 權限

```cmd
icacls "PATH to JDK/JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

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

## <a name="differences-in-ctp-23"></a>CTP 2.3 的差異

如果您已熟悉使用機器學習服務，擴充功能的授權和隔離模型已變更在此版本中。 如需詳細資訊，請參閱 < [SQL Server 機器 2019 Learning Services 安裝中的差異](../install/sql-machine-learning-services-ver15.md)。

## <a name="limitations-in-ctp-23"></a>在 CTP 2.3 的限制

* 輸入和輸出緩衝區中的值數目不能超過`MAX_INT (2^31-1)`因為這是可配置在 Java 中陣列的項目數目上限。

* 輸出中的參數[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)此版本中不支援。

* 使用串流 sp_execute_external_script 參數@r_rowsPerRead此 CTP 中不支援。

* 資料分割使用 sp_execute_external_script 參數@input_data_1_partition_by_columns此 CTP 中不支援。

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>如何從類別檔案中建立的 jar 檔案

瀏覽至包含您的類別檔案的資料夾，然後執行此命令：

```cmd
jar -cf <MyJar.jar> *.class
```

請確定路徑**jar.exe**屬於系統 path 變數。 或者，指定可以找到下 /bin JDK 資料夾中的 jar 的完整路徑： `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 範例](java-first-sample.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)