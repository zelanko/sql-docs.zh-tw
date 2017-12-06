---
title: "更新-SQL Server 文件 Advanced Analytics |Microsoft 文件"
description: "顯示更新的內容，如需 Microsoft SQL server 的進階分析中最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.openlocfilehash: 636e243f1f39f0bfa688c6caada1e03078de9a32
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新增和更新最近： SQL Server 的進階分析



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-09-28** &nbsp; -到- &nbsp; **2017年-12-02**
- *主旨區域：* &nbsp; **Advanced Analytics for SQL Server**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [新增 SQLRUserGroup 為資料庫使用者](r/add-sqlrusergroup-to-database.md)
2. [如何使用 RevoScaleR 函數來尋找或 SQL Server 上的安裝 R 封裝](r/use-revoscaler-to-manage-r-packages.md)
3. [在 Azure SQL Database 中使用 R](r/using-r-in-azure-sql-database.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [機器學習服務中的已知的問題](#TitleNum_1)
2. [使用 miniCRAN 建立本機套件存放庫](#TitleNum_2)
3. [判斷 SQL Server 上已安裝的 R 封裝](#TitleNum_3)
4. [SQL Server 上安裝其他的 R 封裝](#TitleNum_4)
5. [安裝 SQL Server 機器學習在 Azure 虛擬機器上的功能](#TitleNum_5)
6. [安裝預先定型的機器學習模型 SQL Server 上](#TitleNum_6)
7. [避免安裝在使用者程式庫中的 R 封裝上的錯誤](#TitleNum_7)
8. [佈建虛擬機器上 Azure 機器學習](#TitleNum_8)
9. [RevoScaleR](#TitleNum_9)
10. [啟用或停用 SQL Server 的 R 封裝管理](#TitleNum_10)
11. [設定用於 SQL Server 的資料科學用戶端](#TitleNum_11)
12. [設定 SQL Server Machine Learning 服務 (資料庫內)](#TitleNum_12)
13. [自動的安裝的機器學習服務 （資料庫）](#TitleNum_13)
14. [步驟 3：瀏覽及視覺化資料](#TitleNum_14)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1.&nbsp;[機器學習服務中的已知問題](known-issues-for-sql-server-machine-learning-services.md)

*更新日期︰ 2017年-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 321.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00121c648c21576d5c86494137de1d4d81e2e265 c65973f6ae9253af5ecc621916ef36d7c0398789  (PR=3980  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



**Python 程式碼執行，或是 Python 封裝問題**


本節包含專屬於 SQL Server，以及 Microsoft 所發行的 Python 封裝相關的問題上執行 Python 的已知的問題包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

**預先定型的模型的呼叫失敗，則模型路徑太長**


如果您在預設安裝中，視您的電腦名稱和執行個體名稱安裝預先定型的模型定型的模型檔案產生的完整路徑可能會對讀取 Python 而言太長。 這項限制會在服務即將發行版本中修正。

有數個可能的因應措施：

+ 當您安裝的預先定型的模型時，請選擇 自訂位置。
+ 可能的話，請安裝自訂安裝路徑，例如 C:\SQL\MSSQL14 下的 SQL Server 執行個體。MSSQLSERVER。
+ 使用 Windows 公用程式[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)建立永久連結的來源，將模型檔案對應到較短的路徑。

**無法初始化 varbinary 變數 BxlServer 會導致錯誤**


如果您執行 Python 程式碼中使用 SQL Server `sp_execute_external_script`，而且程式碼具有輸出類型 varbinary （max）、 varchar （max） 或類似類型的變數，變數必須初始化，或您的指令碼中設定。 否則，資料 exchange 元件 BxlServer，會引發錯誤並停止運作。

這項限制會在服務即將發行版本中修正。 因應措施，請確定變數會初始化 Python 指令碼內。 可以使用任何有效的值，如下列範例所示：

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-create-a-local-package-repository-using-minicranrcreate-a-local-package-repository-using-minicranmd"></a>2.&nbsp;[建立使用 miniCRAN 本機封裝儲存機制](r/create-a-local-package-repository-using-minicran.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 43.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 44b77cb127e9ffab1777216a66f0e5be9c82f3d2 65e30f10fc36acb3ce95f60f51f3501fbc98ad08  (PR=4150  ,  Filename=create-a-local-package-repository-using-minicran.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



-   **更容易離線安裝**： 若要封裝安裝到離線的伺服器需要，您也可以下載所有套件相依性，使用 miniCRAN 可讓您更輕鬆地取得正確格式的所有相依性。

-   **版本管理改善**： 在多使用者環境中，有合理的原因，若要避免不受限制的伺服器上的多個封裝版本的安裝。

建立儲存機制之後, 您可以藉由新增新的封裝，或升級現有的封裝的版本修改它。

**步驟 1。安裝 miniCRAN 套件**


您開始建立要當做來源使用的 miniCRAN 儲存機制。 您應該可以存取網際網路的電腦上建立這個儲存機制。

1.  安裝 miniCRAN 封裝和所需**igraph**封裝。

```
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
```

**步驟 2。定義封裝來源： CRAN 鏡像或 MRAN 快照集**


1. 指定要用於取得封裝的鏡像網站。

```
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
```

2.  表示用來儲存收集的封裝的本機資料夾。 您不需要命名資料夾 miniCRAN;可能是更具描述性的名稱，例如"GeneticsPackages"或"ClientRPackages1.0.2"。

    只是確定預先建立的資料夾。 如果會引發錯誤`local_repo`資料夾不存在，當您稍後執行的 R 程式碼。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3.&nbsp;[判斷 SQL Server 上已安裝的 R 封裝](r/determine-which-packages-are-installed-on-sql-server.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 13d93acedc6e6b4615f1a244a2a1542910feb69e 9a065066398843a4bed318fa46d4982d712915a9  (PR=4150  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



+ 如果找到封裝，傳回的訊息應該像是 「 命令成功完成。 」

+ 如果不能位於或載入封裝，您會收到如下錯誤: 「 發生外部指令碼錯誤： library("RevoScaleR") 時發生錯誤： 沒有呼叫 RevoScaleR 封裝 」

**取得一份使用 R 的安裝封裝**


有多種方式可以使用 R 工具和 R 函數取得已安裝或已載入封裝的清單。 許多 R 開發工具都提供物件瀏覽器或已在目前 R 工作區中安裝或載入的封裝清單。

+ 從本機的 R 公用程式，使用基底 R 函數，例如`installed.packages()`，隨附於`utils`封裝。 若要取得正確的執行個體的清單，您必須明確地指定程式庫路徑，或使用與執行個體文件庫相關聯的 R 工具。

+ 若要檢查特定的計算內容中的封裝，您可以使用 RevoScaleR 封裝中的下列函式。 這些函式可協助您識別封裝中指定的計算內容：

+ [rxFindPackage (英文)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages (英文)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

例如，執行下列 R 程式碼，以取得指定的 SQL Server 計算內容中可用的封裝清單。

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```
**另請參閱**




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-install-additional-r-packages-on-sql-serverrinstall-additional-r-packages-on-sql-servermd"></a>4.&nbsp;[SQL Server 上安裝其他的 R 封裝](r/install-additional-r-packages-on-sql-server.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 266.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ba48f1838857d90d6692aafc48f393777ac602fa 37de2586a344a99969bcd9a20723c021db2604a4  (PR=4150  ,  Filename=install-additional-r-packages-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



本節提供各種的秘訣和 SQL Server 上的 R 封裝安裝相關的範例程式碼。

**<a name="packageVersion"></a>取得正確的封裝版本和格式**


有多個來源可取得 R 封裝，中其最廣為人知的是 CRAN 和 Bioconductor。 R 語言的官方網站 (<https://www.r-project.org/>) 會列出許多這些資源。 許多封裝會發佈到 GitHub，您可以在這裡取得原始程式碼。 不過，您可能會提供已由公司中的某人所開發的 R 封裝。

不論來源為何，您必須確定您想要安裝的封裝具有二進位格式，以便在 Windows 平台。 否則下載的封裝無法執行 SQL Server 環境中。

在下載之前，您也應該檢查封裝是否與執行 SQL Server 中的 R 版本相容。

**<a name="bkmk_zipPreparation"></a>下載為 zip 檔案的套件**


安裝在沒有網際網路存取的伺服器上，下載離線安裝的 zip 檔案格式的封裝副本。 無法將封裝解壓縮。

例如，下列程序描述現在以取得正確的版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)封裝，從 Bioconductor，假設電腦有網際網路存取權。

1.  在 [Package Archives] (封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下連結。ZIP 檔案，並選取**另存目標**。

3.  瀏覽至本機資料夾壓縮的封裝會儲存位置，而按一下**儲存**。

此程序會建立套件的本機複本。 然後，您可以安裝套件，或將壓縮的封裝複製到沒有網際網路存取的伺服器。

Zip 檔案格式，以及如何建立 R 封裝的內容的相關詳細資訊，我們建議您可以從 R 專案網站的 PDF 格式下載本教學課程：[建立 R 封裝](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-installing-sql-server-machine-learning-features-on-an-azure-virtual-machinerinstalling-sql-server-r-services-on-an-azure-virtual-machinemd"></a>5.&nbsp;[安裝 SQL Server 機器學習在 Azure 虛擬機器上的功能](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f4d287044b8bfda2dbe77fbf65b0d9cdd8f2ff42 2a8e33de6383f5d3af52256c5dfcb60184659eb8  (PR=4150  ,  Filename=installing-sql-server-r-services-on-an-azure-virtual-machine.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



6. 如果您打算從遠端資料科學用戶端連接的執行個體時，完成 [額外的步驟-#additional-步驟） 為必要。

**停用 SQL Server VM 上的機器學習功能**


您也可以啟用或停用現有的 SQL Server 虛擬機器上的功能，在任何時間。

1. 開啟虛擬機器刀鋒視窗。
2. 按一下 [設定]，並選取 [SQL Server 組態]。
3. 對功能進行變更，並套用。

**<a name="existing"></a>將 R 服務新增到現有的 SQL Server 2016 Enterprise VM**


如果您建立 Azure 機器學習服務不包含 SQL Server 虛擬機器，您可以加入功能，依照下列步驟：

1. 重新執行..！裡 NotShown-v.../../includes/ssnoversion-md.md)] 設定，並將功能加入**伺服器組態**精靈頁面。
2. 啟用執行外部指令碼並重新啟動 … ！裡 NotShown-v.../../includes/ssnoversion-md.md)] 的執行個體。 如需詳細資訊，請參閱 [設定設定 SQL Server R 服務../../ advanced-analytics/r/set-up-sql-server-r-services-in-database.md）。
3. (選擇性) 如果遠端指令碼執行需要，請設定 R 背景工作帳戶的資料庫存取權。
   如需詳細資訊，請參閱 [設定設定 SQL Server R 服務../../ advanced-analytics/r/set-up-sql-server-r-services-in-database.md）。
3. (選擇性) 如果您想要允許從遠端資料科學用戶端執行 R 指令碼，請修改 Azure 虛擬機器上的防火牆規則。 如需詳細資訊，請參閱 [解除封鎖防火牆-#firewall）。
4. 安裝或啟用必要的網路程式庫。 如需詳細資訊，請參閱 [新增網路通訊協定-#network）。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-install-pretrained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>6.&nbsp;[安裝預先定型的 SQL Server 上的機器學習模型](r/install-pretrained-models-sql-server.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 96.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07b51584a90568cccceea382c44155e40e09c967 db083f8536fbb2ea5886fed787872867b5de5750  (PR=4150  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    For example, to enable use of the latest version of the pretrained models for Python, in a default instance of SQL Server 2017, you would run this statement:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    On a named instance, the command would be something like this:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + 若要使用 Python 預先定型模型使用機器學習 Server （獨立）：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    例如，假設使用 SQL Server 2017 安裝程式的預設安裝的機器學習伺服器 （獨立），執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. 版本參數支援下列值：



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-avoiding-errors-on-r-packages-installed-in-user-librariesrpackages-installed-in-user-librariesmd"></a>7.&nbsp;[避免使用者文件庫中安裝 R 封裝上的錯誤](r/packages-installed-in-user-libraries.md)

*更新日期︰ 2017年-10-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 52cb9a53d7d9c31ee9bc6977464ebd2a18081ff3 3537aa6755c66f12c19bb3448dc9b5c8abb9cc28  (PR=3619  ,  Filename=packages-installed-in-user-libraries.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=aecf422ca2289b2a417147eb402921bb8530d969) -->



不過，這可以永遠不會運作，SQL Server 中執行 R 解決方案時因為安裝 R 封裝，至特定的預設文件庫的執行個體相關聯。

如果封裝並未安裝於預設程式庫中，您可能會在嘗試呼叫封裝時發生這個錯誤：

*Library(xxx) 時發生錯誤： 沒有名為 ' 封裝 name' 的封裝*

也不正確的開發做法是必要的 R 封裝安裝至自訂使用者文件庫，因為如果沒有存取程式庫位置的另一個使用者所執行的方案，它會導致錯誤。

**如何安裝 R 封裝至可存取的文件庫**


**適用於 SQL Server 2016**

使用執行個體相關聯的套件程式庫。 如需詳細資訊，請參閱 [使用 SQL Server--installing-and-managing-r-packages.md 安裝 R 封裝）

**適用於 SQL Server 2017**

SQL Server 提供功能，可協助您管理多個封裝版本，並提供使用者的權限給個別的封裝，而不需要使用者具有檔案系統存取權。

如需如何設定共用的封裝程式庫，並將使用者指派給角色的詳細資訊，請參閱 [R 封裝管理 SQL Server--r-package-management-for-sql-server-r-services.md。）




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-provision-a-virtual-machine-for-machine-learning-on-azurerprovision-the-r-server-only-sql-server-2016-enterprise-vm-on-azuremd"></a>8.&nbsp;[佈建虛擬機器上 Azure 機器學習](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

*更新日期︰ 2017年-10-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_7) | [下一步](#TitleNum_9))

<!-- Source markdown line 132.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 16439b4a8f5f4218edfcd746ed20ccbc8263dabc 1b3a8a7d1ceceaa459b3fd5640da26859df8d80b  (PR=3748  ,  Filename=provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=262e3cf5df2448bb6b532c0549c3d72daefe5a96) -->



|名稱| 註解|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise on Windows|整合式的進階分析的 R 服務。|
|BYOL SQL Server 2016 SP1 Enterprise on Windows Server |整合式的進階分析的 R 服務。 |
|Windows Server 2016 上可用的授權： SQL Server 2016 SP1 Developer |整合式的進階分析的 R 服務。 |
| Data Science 虛擬機器 Windows 2012|包含常用的工具，用於資料科學，包括 Microsoft R Server Developer Edition、 SQL Server 2016 Developer edition、 Anaconda Python 發佈、 Julia Pro developer edition 和 Jupyter 筆記本如。|
| Data Science 虛擬機器 Windows 2016|包含 SQL Server 2016 Developer Edition 支援資料庫內部 R 分析。|
|**SQL Server 2017**| ***   |
|SQL Server 2017 企業的 Windows Server 2016| 機器學習服務，具有 Python 和 R 語言支援。|
|BYOL SQL Server 2017 企業的 Windows Server 2016|機器學習服務，具有 Python 和 R 語言支援。|
| 在 Windows 伺服器上可用的 SQL Server 授權： SQL Server 2017 Developer|機器學習服務，具有 Python 和 R 語言支援。|
| **其他**| *** |
| 機器學習伺服器只有 SQL Server 2017 Enterprise|類似於 SQL Server 2016 Enterprise 映像，但包含 Server 機器學習的獨立版本，並有核心 ScaleR 和實施功能適用於 Windows 的環境最佳化。|
| 機器學習 Server for Windows|獨立伺服器的版本機器學習，含有實施最佳化 Windows 環境的功能。|



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-revoscalerrrevoscaler-overviewmd"></a>9.&nbsp;[RevoScaleR](r/revoscaler-overview.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_8) | [下一步](#TitleNum_10))

<!-- Source markdown line 18.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 92f2dfa2e75037a932415881c55d2fd37fc6847a c6e9f17f2df82447b18beff41769ae3ebfbed562  (PR=4150  ,  Filename=revoscaler-overview.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->




RevoScaleR 是 Microsoft 支援大規模的資料科學所提供的機器學習服務函數封裝。

+ 函數支援資料匯入、 資料轉換、 摘要、 視覺化和分析。

+ _大規模_表示作業會針對極大型資料集，以平行方式，執行，而且在分散式檔案系統。 演算法可在不適合在記憶體中，藉由使用區塊處理和 reassembling 結果完成作業時的資料集上操作。

+ RevoScaleR 透過開放原始碼 R 函式提供多項改良。 沒有對應到多個最受歡迎的基底 R 函數的 RevoScaleR 函式。 RevoScaleR 函數皆加註**rx**或**Rx**前置詞，使其更容易識別。

+ RevoScaleR 作為分散式的資料科學的平台。 比方說，您可以使用 RevoScaleR 計算內容和轉換中的圖案狀態演算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)。 您也可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)以平行方式執行基底 R 函數。

RevoScaleR 的作用中的範例，請參閱這些部落格：

+ [建置和部署使用 R 和 SQL Server 的預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [機器學習伺服器每秒 100 萬個預測](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [預測使用 MicrosoftML 計程車秘訣](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [效能最佳化的 rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

**如何取得 RevoScaleR**




&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-enable-or-disable-r-package-management-for-sql-serverrr-package-how-to-enable-or-disablemd"></a>10.&nbsp;[啟用或停用 SQL Server 的 R 封裝管理](r/r-package-how-to-enable-or-disable.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_9) | [下一步](#TitleNum_11))

<!-- Source markdown line 60.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f846cd7d601459a95e694ada41e9fc5285f3de9 83a4a84adf47670c7fd4599f889f27ec3c219708  (PR=4150  ,  Filename=r-package-how-to-enable-or-disable.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    If you do not specify a user, the current security context is used.

3. 每個資料庫必須已安裝封裝中重複命令。

4.  若要確認已成功建立新的角色，在 SQL Server Management Studio 中，按一下資料庫，展開 **安全性**，然後展開**資料庫角色**。

    您也可以執行的查詢上 sys.database_principals 如下所示：

```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,
        pr.authentication_type_desc, pe.state_desc,
        pe.permission_name, s.name + '.' + o.name AS ObjectName
    FROM sys.database_principals AS pr
    JOIN sys.database_permissions AS pe
        ON pe.grantee_principal_id = pr.principal_id
    JOIN sys.objects AS o
        ON pe.major_id = o.object_id
    JOIN sys.schemas AS s
        ON o.schema_id = s.schema_id;
```

4.  任何具有適當的權限的使用者尚未啟用的功能之後，可以使用[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)T-SQL 加入封裝中的陳述式。 如需其運作方式的範例，請參閱[SQL Server 上安裝其他封裝](r/install-additional-r-packages-on-sql-server.md)。

**<a name="bkmk_disable"></a>停用封裝管理**




&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-set-up-a-data-science-client-for-use-with-sql-serverrset-up-a-data-science-clientmd"></a>11.&nbsp;[設定搭配 SQL Server 的資料科學用戶端](r/set-up-a-data-science-client.md)

*更新日期︰ 2017年-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_10) | [下一步](#TitleNum_12))

<!-- Source markdown line 52.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f674f5d329211e4c7d8dc464bd70f1cdef633350 8c65fc96c04f32d1e4777870774a11f9fd2ee219  (PR=3765  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



    For setup information, see [How to install R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

    To configure RTVS to use your Microsoft R client libraries, see [About Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    即使免費的 Community Edition 包含資料科學工作負載，安裝適用於 R、 Python 和 F # 專案範本。

    下載 Visual Studio 從[此站台](https://www.visualstudio.com/vs/)。

+ RStudio

    如果您偏好使用 RStudio，需要一些額外步驟才能使用 RevoScaleR 程式庫︰

    - 安裝 Microsoft R 用戶端，以取得需要的套件和程式庫。
    - 更新您的 R 路徑，以便使用 Microsoft R 執行階段。

    如需詳細資訊，請參閱[R 用戶端-設定您的 IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide)。

**設定您的 IDE**


+ 適用於 Visual Studio 的 R 工具

    請參閱[此站台](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)如需如何建置和偵錯 R 的一些範例專案中使用 R Tools for Visual Studio。

+ Visual Studio 2017

    如果您安裝 Microsoft R 用戶端或 R 伺服器**之前**您安裝 Visual Studio、 「 R 伺服器程式庫會自動偵測與用於程式庫路徑。 如果您尚未安裝 RevoScaleR 程式庫中，從**R 工具**功能表上，選取**安裝 R 用戶端**。

**SQL Server 中執行 R**


這個範例會使用 Visual Studio 2017 Community Edition 中，以安裝資料科學工作負載。

1. 從**檔案**功能表上，選取**新增**，然後選取 **專案**。

2. -手形窗格包含預先安裝的範本清單。 按一下**R**，然後選取**R 專案**。 在**名稱**方塊中，輸入`dbtest`按一下**確定**。



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>12.&nbsp;[設定 SQL Server 機器學習服務 （資料庫）](r/set-up-sql-server-r-services-in-database.md)

*更新日期︰ 2017年-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_11) | [下一步](#TitleNum_13))

<!-- Source markdown line 111.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4d355f6494b417dd90dce3943e7176eaece7336e 20bddb8ffd4cf3774b812a7376c70b95ccc57e92  (PR=3980  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



   + Database Engine 服務
   + R 服務 (資料庫內)

7. 安裝完成時，重新啟動電腦。


**<a name="bkmk2017top"></a>安裝 SQL Server 2017 機器學習服務 （資料庫）**


> [!div class="checklist"]
> * 安裝 database engine 和機器學習功能
> * 需要後續安裝步驟： 啟用 machine learning 中，然後重新啟動
> * 選擇性的後續安裝步驟： 加入防火牆規則，將使用者加入、 變更或設定服務帳戶設定的遠端資料科學用戶端。

**開始使用**

1. 執行..！裡 NotShown-v.../../includes/ssnoversion-md.md)] 的安裝程式。

2. 在**安裝**索引標籤上，選取**新的 SQL Server 獨立安裝或將功能加入現有安裝**。

     ![安裝機器學習服務 (In-Database)--media/2017setup-installation-page-mlsvcs.png 「 機器學習服務與啟動安裝資料庫引擎 」)

3. 在**特徵選取**頁面上，選取下列選項：

    + 選取**Database Engine Services**。 需要資料庫引擎使用機器學習的每個執行個體。

    + 選取**機器學習服務 （資料庫）**。 此選項會安裝支援的資料庫中使用。選取此選項之後，您可以選取的機器學習語言。 您可以選取只 R，或者您可以加入 R 和 Python。

    ![Selection--media/2017setup-features-page-mls-rpy.png 的機器學習服務功能 」 選取這些功能的 R 服務中的資料庫 」)

    如果您未選取 [R] 或 [Python 語言選項，安裝精靈正在安裝只能擴充性架構，其中包含 SQL Server 受信任的啟動列]，並不會安裝任何語言特有的元件。  通常我們建議您開始安裝至少一種語言。 不過，您可能會使用此選項，如果您想要立即升級機器學習元件使用的繫結程序。 如需詳細資訊，請參閱 [使用 SqlBindR R Services--use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md 的執行個體升級。)



&nbsp;

&nbsp;

---

<a name="TitleNum_13"/>

### <a name="13-nbsp-unattended-installation-of-machine-learning-services-in-databaserunattended-installs-of-sql-server-r-servicesmd"></a>13.&nbsp;[自動的安裝的機器學習服務 （資料庫）](r/unattended-installs-of-sql-server-r-services.md)

*更新日期︰ 2017年-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_12) | [下一步](#TitleNum_14))

<!-- Source markdown line 75.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ad203c90adff3f515b5f16472fad9753be7a421d 6925a9276bcd4a80babc7504de50400f1a5a2940  (PR=3765  ,  Filename=unattended-installs-of-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



下列範例會示範使用加入 Python 語言安裝的 SQL Server 2017 機器服務 （資料庫） 的執行無訊息方式，自動安裝所需的引數。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

請注意在 SQL Server 2017 Python 所需的旗標：

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

**具名執行個體上安裝 R 和 Python**


下列範例會示範執行無訊息方式，自動安裝所需的引數安裝 SQL Server 2017 機器 Services （資料庫） 的具名執行個體上。 會加入 R 和 Python 語言。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

**<a name="OldInstall"></a>SQL Server 2016 命令列安裝**


下列範例示範加入之 R 語言安裝的 SQL Server 2016 的執行無訊息方式，自動安裝所需的引數。



&nbsp;

&nbsp;

---

<a name="TitleNum_14"/>

### <a name="14-nbsp-step-3-explore-and-visualize-the-datatutorialssqldev-py3-explore-and-visualize-the-datamd"></a>14.&nbsp;[步驟 3： 瀏覽及視覺化資料](tutorials/sqldev-py3-explore-and-visualize-the-data.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_13))

<!-- Source markdown line 66.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 47edcfbd8da7cf1ea1ad03a05f86d3cd26014827 674a7c7d0e8290fc91970ed2aeda3b97d5165d75  (PR=4150  ,  Filename=sqldev-py3-explore-and-visualize-the-data.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    Class 4: `tip_amount` > $20

**建立 T-SQL 中使用 Python 的繪圖**


開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 由於視覺效果是這種功能強大的工具來了解在極端值與資料的分佈，Python 提供許多封裝將資料視覺化。 **Matplotlib**模組是其中一個視覺效果中，常見的程式庫，而且包含了許多函數，可建立長條圖、 散佈圖、 方塊繪圖和其他資料瀏覽圖形。

在本節中，您可以了解如何搭配使用預存程序的繪圖。 而是比開啟伺服器上的映像，您將 Python 物件儲存`plot`為**varbinary**資料，以及該檔案，可以是共用或其他地方檢視再寫入。

**建立圖做為 varbinary 資料**


**Revoscalepy**模組隨附於 SQL Server 2017 機器學習服務支援的功能類似於**RevoScaleR**的 r 封裝 這個範例會使用 Python 相當於`rxHistogram`来繪製的長條圖的資料...！裡 NotShown-tsql.../../includes/tsql-md.md)] 的查詢。

預存程序會傳回已序列化的 Python`figure`物件做為資料流**varbinary**資料。 您無法直接管理，檢視的二進位資料，但是您可以使用用戶端上的 Python 程式碼，以還原序列化，並檢視數字，並再儲存在用戶端電腦的映像檔案。

1. 建立預存程序_SerializePlots_，如果 PowerShell 指令碼未已經這樣做。

    - 變數`@query`定義的查詢文字`SELECT tipped FROM nyctaxi_sample`，為指令碼輸入變數的引數傳遞給 Python 程式碼區塊`@input_data_1`。
    - Python 指令碼是相當簡單： **matplotlib** `figure`物件可用來讓色階分佈圖和散佈圖，這些物件會接著使用序列化`pickle`程式庫。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 14): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (87 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (5 + 4):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (2 + 2): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (10 + 9): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (2 + 4):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (4 + 2): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 1):**範例 sql**文件](../sample/new-updated-sample.md)
- [新 + 更新 (21 + 0): **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (5 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新 + 更新 (0 + 0):**資料移轉小幫手 (DMA) sql**文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


