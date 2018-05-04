---
title: 更新-SQL Server 文件 Advanced Analytics |Microsoft 文件
description: 顯示更新的內容，如需 Microsoft SQL server 的進階分析中最近變更過的文件的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 04/28/2018
ms.openlocfilehash: bbce32579b54647e167c25d2708a80027ae0e678
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新增和更新最近： SQL Server 的進階分析



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2018年-02-03** &nbsp; -到- &nbsp; **2018年-04-28**
- *主旨區域：* &nbsp; **Advanced Analytics for SQL Server**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


1. [安裝 SQL Server 2017 機器學習在 Windows 上的服務 （資料庫）](install/sql-machine-learning-services-windows-install.md)
2. [安裝 SQL Server 2017 機器學習 Windows 上的伺服器 （獨立）](install/sql-machine-learning-standalone-windows-install.md)
3. [從命令列安裝 SQL Server 機器學習服務元件](install/sql-ml-component-commandline-install.md)
4. [安裝 SQL Server 機器學習服務沒有網際網路存取的元件](install/sql-ml-component-install-without-internet-access.md)
5. [安裝 SQL Server 2016 R Services （資料庫）](install/sql-r-services-windows-install.md)
6. [安裝 SQL Server 2016 R Server （獨立）](install/sql-r-standalone-windows-install.md)
7. [設定用戶端工具，搭配 SQL Server 機器學習使用 Python](python/setup-python-client-tools-sql.md)
8. [在 SQL 中使用 Python 模型，用於定型和計分](tutorials/train-score-using-python-in-tsql.md)
9. [Python 程式碼包裝在預存程序](tutorials/wrap-python-in-tsql-stored-procedure.md)
10. [什麼是 SQL Server 機器學習服務？](what-is-sql-server-machine-learning.md)
11. [監視 PREDICT 陳述式的擴充事件](xe-event-predict-tsql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [檢視 R 或 SQL Server 上安裝的 Python 封裝](#TitleNum_1)
2. [安裝預先定型的機器學習模型 SQL Server 上](#TitleNum_2)
3. [設定 SQL Server 上的 R 開發資料科學用戶端](#TitleNum_3)
4. [SQL Server 機器學習和 R 服務 （資料庫）](#TitleNum_4)
5. [執行 Python 使用 T-SQL](#TitleNum_5)
6. [使用 Python revoscalepy 建立模型](#TitleNum_6)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-viewing-r-or-python-packages-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>1.&nbsp; [檢視 R 或 SQL Server 上安裝的 Python 封裝](r/determine-which-packages-are-installed-on-sql-server.md)

*更新日期︰ 2018年-04-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 208.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f ec6859ac91b27539dc36f21aec82c99937c0187a  (PR=5610  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f1f96a990644c0d6cfa5a1d88ccee959cab6c2b2) -->



**Python**


這個範例會傳回包含在 Python 的資料夾清單`sys.path`變數。 此清單包含目前的目錄和標準程式庫路徑。

```
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**結果**

```
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

如需有關變數`sys.path`以及如何它用來設定模組，解譯器搜尋路徑，請參閱[Python 文件](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-install-pre-trained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>2.&nbsp; [安裝預先定型的機器學習模型 SQL Server 上](r/install-pretrained-models-sql-server.md)

*更新日期︰ 2018年-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 140.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 aa03623d819750d4919feb7910b07ec1875bb509 7382228fa68b04b500a5fde73c29995e12aa20ac  (PR=5504  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



1. 啟動個別的 windows 安裝程式針對[R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)或[Server 機器學習](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 選取您想要更新，然後選取的語言**Pre-trained 模型**選項。

    > [!TIP]
    > 如果您先前已執行安裝程式更新 R 伺服器 （獨立），而且只想要將預先定型的模型，保留所有先前的選取項目**現狀**，然後選取剛才預先 **-定型模型**選項. **不這麼做**取消選取任何先前選取的選項; 如果您這樣做時，安裝程式會移除元件。

    我們建議您接受模型位置的預設設定。

3. 按一下 **[繼續]**。

4. 接受所有其他提示，包括授權合約。

安裝完成之後，您必須執行一些額外的步驟來註冊預先定型的模型。

1. 開啟 Windows 命令提示字元**以系統管理員身分**。

2. R 伺服器 （獨立），其中也包含 Microsoft R 安裝程式，瀏覽至安裝程式啟動載入器資料夾。

3. 執行`RSetup.exe`和表示要安裝的元件、 版本，以及包含模型的來源檔案，使用此語法的資料夾：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    版本參數支援下列值：



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-set-up-a-data-science-client-for-r-development-on-sql-serverrset-up-a-data-science-clientmd"></a>3.&nbsp; [設定 SQL Server 上的 R 開發資料科學用戶端](r/set-up-a-data-science-client.md)

*更新日期︰ 2018年-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 39.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0583f8febcedc5dc2e14ca1a8073ca204ca37987 3d50ad8f35f2985944741a9b2211a461df2c13e4  (PR=5504  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



**R 工具**


當您安裝 R 與 SQL Server 時，您會收到相同與任何已安裝的 R 工具**基底**R，例如 RGui、 Rterm，以及其他等等的安裝。 因此技術上來說，您必須開發和測試 R 程式碼所需的所有工具。

下列標準的 R 工具隨附的*基底安裝*，並因此預設會安裝。

+ **RTerm**： 命令列的終端機執行 R 指令碼

+ **RGui.exe**：R 的簡單互動式編輯器。RGui.exe 和 RTerm 的命令列引數相同。

+ **RScript**：以批次模式執行 R 指令碼的命令列工具。

若要尋找這些工具，決定當您設定 SQL Server 或獨立機器學習功能已安裝的 R 程式庫。 比方說，在預設安裝中，R 工具都在這些資料夾位於：

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server 的獨立： `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 機器學習服務： `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ 機器學習服務伺服器 （獨立）： `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

如果您需要協助的 R 工具，直接開啟**RGui**，按一下 **協助**，然後選取其中一個選項

**Microsoft R Client**


Microsoft R 用戶端是免費下載，可讓您存取以供開發使用 RevoScaleR 封裝。 安裝 R 用戶端，您可以建立可以在所有支援的計算內容，包括 SQL Server 資料庫中的分析，以及 Hadoop、 Spark 或使用機器學習伺服器 Linux 上的分散式 R 運算執行的 R 解決方案。

如果您已經安裝不同的 R 開發環境，例如 RStudio，務必要使用的程式庫和 Microsoft R 用戶端所提供的可執行檔的環境重新設定。 藉由讓您可以使用 RevoScaleR 封裝中，所有的功能但效能會受到限制。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sql-server-machine-learning-and-r-services-in-databasersql-server-r-servicesmd"></a>4.&nbsp; [SQL Server 機器學習和 R 服務 （資料庫）](r/sql-server-r-services.md)

*更新日期︰ 2018年-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 83.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b1a95a7f6d391a518762eb271e8ea7e0d684d403 7fbfabf62917e03e2bcb99d297e1c9d0f0604440  (PR=5504  ,  Filename=sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



選擇工作的最佳語言。 R 最適用於統計計算很難使用 SQL 實作。 透過資料的集合式作業，利用 *{包含內容-傳送-這裡}* 達到最佳效能。 使用記憶體中資料庫引擎非常快速的計算資料行。

**步驟 4： 最佳化您的方案**


模型上的企業資料縮放就緒時，資料科學家通常運作方式與 DBA 或 SQL 開發人員最佳化程序，例如：

+ 特徵工程
+ 擷取資料和資料轉換
+ 計分

傳統上使用 R 的資料科學家會有問題的效能和延展性，尤其是使用大型資料集。 這是因為通用執行階段實作是單一執行緒，而且可以容納放入本機電腦上的可用記憶體的資料集。 與 SQl Server 機器學習服務整合提供多項功能，以提升效能、 更多資料：

+ **RevoScaleR**： 此 R 封裝包含某些熱門 R 函數，經過重新設計可提供平行處理原則與規模的實作。 此封裝包含函式，以進一步提升效能與延展性，透過將計算推送至 *{包含內容-傳送-這裡}* 通常會有記憶體更大且運算能力的電腦。

+ **revoscalepy**。 此 Python 程式庫，提供 SQL Server 2017，實作 RevoScaleR 中, 最受歡迎的函式，例如遠端計算內容和許多支援的演算法分散式處理。

**資源**

+ [效能案例研究]
+ [R 和資料最佳化]

**步驟 5： 部署和使用**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-run-python-using-t-sqltutorialsrun-python-using-t-sqlmd"></a>5.&nbsp; [執行 Python 使用 T-SQL](tutorials/run-python-using-t-sql.md)

*更新日期︰ 2018年-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 306.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bde8c6476df259d225847c08224cefd02f3529d5 cad56997abe7928b588ac4a0302384c5edc1ede5  (PR=5497  ,  Filename=run-python-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



2. 請注意索引值不是輸出，即使您使用索引來從 data.frame 取得特定的值。

    **結果**

    |ResultValue|
    |------|
    |0.5|
    |2|

**使用索引的 data.frame 輸出值**


我們來看看使用我們的兩個數列包含簡單的數學運算的結果轉換成 data.frame 的運作方式。 第一個有 Python 所產生的循序值的索引。 第二個會使用任意字串值的索引。

1. 這個範例會取得值，從序列的整數索引。

```
    EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
```

請記住，自動產生索引 0 開始。 請嘗試使用超出範圍的索引值，請參閱 會發生什麼事。

2. 現在讓我們從具有字串索引的其他資料框架中取得單一值。

```
    EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
```

**結果**

|ResultValue|
|------|
|0.5|

如果您嘗試使用的數字索引，以取得此系列中的值，您會收到錯誤。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>6.&nbsp; [使用 Python revoscalepy 建立模型](tutorials/use-python-revoscalepy-to-create-model.md)

*更新日期︰ 2018年-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_5))

<!-- Source markdown line 22.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5b642b391ca571412c30c8470875d3d4d3c57246 bd83387eb8a1076a1396bbd48dca12872843aa2f  (PR=5497  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



如果您安裝的 SQL Server 2017 發行前版本，您應該更新為至少 RTM 版本。 以展開和改善 Python 功能持續更新的服務版本。 本教學課程的某些功能可能不適用於早期發行前版本。

+ 這個範例會使用預先定義的 Python 環境，名為`PYTEST_SQL_SERVER`。 在環境已設定為包含**revoscalepy**及其他必要的程式庫。

    如果您沒有設定為執行 Python 環境，您必須個別執行。 如何建立或修改 Python 環境的討論超出本教學課程的範圍。 如需如何設定包含正確的程式庫的 Python 用戶端的詳細資訊，請參閱[安裝 Python 用戶端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)和[連結的 Python 工具](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。

**遠端計算內容和 revoscalepy**


此範例將示範如何在遠端建立 Python 模型的程序_計算內容_，可以讓您從用戶端，但選擇遠端環境，例如 SQL Server、 Spark 或機器學習伺服器，其中作業會實際執行。 使用的計算內容，可以更輕鬆地撰寫程式碼一次，並將它部署到任何支援的環境。

若要在 SQL Server 中執行 Python 程式碼需要**revoscalepy**封裝。 這是特殊的 Python 封裝，類似於 Microsoft 提供的**RevoScaleR**的 R 語言套件。 **Revoscalepy**套件支援建立的計算內容和提供的基礎結構，用來在本機工作站與遠端伺服器之間傳遞資料和模型。 **Revoscalepy**函式的支援的資料庫中的程式碼執行[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (11 + 6): &nbsp; &nbsp; **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (18 + 0): &nbsp; &nbsp; **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (218 + 14):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (14 + 0): &nbsp; &nbsp; **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (3 + 2): &nbsp; &nbsp; **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (3 + 3): &nbsp; &nbsp; **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (7 + 10): &nbsp; &nbsp;**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 2): &nbsp; &nbsp; **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 3): &nbsp; &nbsp; **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): &nbsp; &nbsp; **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (1 + 1): &nbsp; &nbsp; **Tools for SQL**文件](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新 + 更新 (0 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 0): **SQL 的 Data Quality Services**文件](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**資料採礦延伸模組 (DMX)，sql**文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多維度運算式 (MDX) 的 SQL**文件](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **ODBC （開放式資料庫連接） 的 SQL**文件](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**適用於 SQL PowerShell**文件](../powershell/new-updated-powershell.md)
- [新 + 更新 (0 + 0):**範例 sql**文件](../samples/new-updated-samples.md)
- [新 + 更新 (0 + 0): **SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新 + 更新 (0 + 0): **sql XQuery**文件](../xquery/new-updated-xquery.md)

