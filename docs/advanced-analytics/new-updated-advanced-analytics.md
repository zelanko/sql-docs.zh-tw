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
ms.date: 09/11/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fb6185aae04a1fb53a4db03cbab267e3f52dc779
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新增和更新最近： SQL Server 的進階分析



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-07-18** &nbsp; -到- &nbsp; **2017年-09-11**
- *主旨區域：* &nbsp; **Advanced Analytics for SQL Server**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結跳至最近新增的新發行項。


1. [如何執行即時計分或 SQL Server 中的原生計分](r/how-to-do-realtime-scoring.md)
2. [安裝預先定型的機器學習模型 SQL Server 上](r/install-pretrained-models-sql-server.md)
3. [原生評分](sql-native-scoring.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

此區段會顯示更新所收集從最近曾發生大規模的更新發行項的摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單所提供的摘錄的一節中所列的所有更新文章連結。

1. [設定 Python 機器學習服務 （資料庫）](#TitleNum_1)
2. [介紹 revoscalepy](#TitleNum_2)
3. [SQL Server 版本間的機器學習服務功能差異](#TitleNum_3)
4. [實施 R 程式碼 （機器學習服務）](#TitleNum_4)
5. [R 服務的效能： 結果和資源](#TitleNum_5)
6. [R Services-資料最佳化的效能](#TitleNum_6)
7. [SQL Server 的 R 封裝管理](#TitleNum_7)
8. [設定 SQL Server Machine Learning 服務 (資料庫內)](#TitleNum_8)
9. [使用 R 與 SQL Server 組態](#TitleNum_9)
10. [SQL Server 中 R 的效能微調](#TitleNum_10)
11. [資料科學案例和解決方案範本](#TitleNum_11)
12. [新功能 SQL Server 中的機器學習服務](#TitleNum_12)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-set-up-python-machine-learning-services-in-databasepythonsetup-python-machine-learning-servicesmd"></a>1.&nbsp;[設定 Python 機器學習服務 （資料庫）](python/setup-python-machine-learning-services.md)

*更新日期︰ 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 263.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 fbe2ef55a5caecd64bb21ce854617a10b2d65567 8cd65baf77f27db00a0a4f07f3129a4231edb48b  (PR=3084  ,  Filename=setup-python-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=05976158e43d7dfafaf02289462d1537f5beeb36) -->



     [Modify the user account pool for SQL Server R Services--../r/modify-the-user-account-pool-for-sql-server-r-services.md)

如果您使用 SQL Server Standard Edition，且沒有資源管理員，您可以使用動態管理檢視和擴充的事件，可協助您管理伺服器資源。 您也可以使用 Windows 事件監視針對此目的。 如需詳細資訊，請參閱 [監視和管理 R 服務../r/managing-and-monitoring-r-solutions.md)。

**升級的機器學習服務元件**


當您使用 SQL Server 2017 安裝機器學習服務時，您會取得元件的版本在發行版本時的時間。 每次您更新或升級 SQL Server 執行個體的機器學習元件也會升級。

您可以升級的機器學習服務元件快排程超過支援的 SQL Server 版本中，藉由安裝 Microsoft 機器學習的伺服器。 當您這樣做時，您也可以取得支援最新版的機器學習伺服器，任何新功能：

+ Python 封裝更新[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。
+ [預先定型模型](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)影像分類和文字分析。

如需如何升級執行個體，請參閱 [透過繫結-升級 R 元件...\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

> [!NOTE]
>
> 目前的發行版本包含所有的機器學習服務元件的最新版本。 因此，儘管支援透過 Microsoft 機器學習伺服器升級為 SQL Server 2017，目前可用升級只適用於 SQL Server 2016 執行個體。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>2.&nbsp;[簡介 revoscalepy](python/what-is-revoscalepy.md)

*更新日期︰ 2017年-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 79.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a d2eac3313a74bc5d5afd754fc357b3693e6801e1  (PR=2939  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



| (column_1) | (column_2) | (column_3) |
| :-- | :-- | :-- |
|`rx_btrees` | 符合隨機梯度促進式的決策樹|`rx_btrees_ex`在 CTP 2.0|
|`rx_dforest` | 符合分類和迴歸的決策樹系|`rx_dforest_ex`在 CTP 2.0|
|`rx_dtree` | 調整的分類和迴歸樹狀結構 |`rx_dtree_ex`在 CTP 2.0|
|`rx_lin_mod` | 建立線性模型|`rx_lin_mod_ex`在 CTP 2.0|
|`rx_logit` | 建立羅吉斯迴歸模型|`rx_logit_ex`在 CTP 2.0|
|`rx_predict` | 產生從定型模型的預測|`rx_predict_ex`在 CTP 2.0|
|`rx_summary` | 產生模型的摘要||

新的機器學習演算法也會提供的 Python 版本[MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| 函數| Description|
| ------ | ------ |
|`rx_fast_forest` |建立決策樹系模型|
|`rx_fast_linear` | 線性迴歸與隨機雙重座標 （堆疊）|
|`rx_fast_trees` | 建立促進式樹狀結構的模型 |
|`rx_logistic_regression` | 建立羅吉斯迴歸模型|
|`rx_neural_network` | 建立可自訂類神經網路模型 |
|`rx_oneclass_svm` | 平衡資料集，以用於異常偵測上建立 SVM 模型|

> [!TIP]
> 許多這些演算法已提供做為 Azure Machine Learning 中的模組。

Python MicrosoftML 也包括各種不同的轉換和 helper 函式，例如：

+ `rx_predict`產生從定型模型的預測，而且可以用於即時計分
+ 映像功能，其潛在函式
+ 進行文字處理和人氣擷取函式

如需詳細資訊，請參閱[MicrosoftML 簡介](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 社群使用可能不同於您所用，包括所有小寫字母和底線，而非 camel 命名法的大小寫的參數名稱的程式碼撰寫慣例。 此外，也許您注意到， **revoscalepy**程式庫一律為小寫。 沒錯 ！ 其他的 Python 慣例。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-differences-in-machine-learning-features-between-editions-of-sql-serverrdifferences-in-r-features-between-editions-of-sql-servermd"></a>3.&nbsp;[機器學習功能的 SQL Server 版本之間的差異](r/differences-in-r-features-between-editions-of-sql-server.md)

*更新日期︰ 2017年-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 47.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5890e212063f3ef228e69afe54e226320d2467f 4e0357701d960c0b8dbda1ac8d56a82f3335c77f  (PR=2964  ,  Filename=differences-in-r-features-between-editions-of-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



     Only Express Edition with Advanced Services includes the machine learning features. The performance limitations are similar to Standard Edition. Web edition is not intended for tasks such as creating machine learning models; however, you can use the PREDICT function to perform scoring using models trained elsewhere.

-   **Azure SQL Database**

     在 Azure SQL Database 目前不支援機器學習功能，例如 R，並將 Python 指令碼。

     如需詳細資訊和相關當此功能即將，公告，請參閱 SQL Server 部落格： [Python 中 SQL Server 2017： 增強式資料庫中的機器學習服務](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


**所有版本中支援的語言**


所有版本都支援下列機器學習語言：

+ SQL Server 2017: R 和 Python
+ 只有 SQL Server 2016: R

Microsoft R Open 包含在所有版本內。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-operationalize-r-code-machine-learning-servicesroperationalizing-your-r-codemd"></a>4.&nbsp;[實施 R 程式碼 （機器學習服務）](r/operationalizing-your-r-code.md)

*更新日期︰ 2017年-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e11d9a5db93932ec89ca96b5337aa4ea03c1d13 0779f06444b5b73ae2dff8bc190d0e388b4ae8e7  (PR=2660  ,  Filename=operationalizing-your-r-code.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



+ [即時../ 即時單次 scoring.md） 小批次計分，最佳化
+ 單一資料列計分，用於呼叫從應用程式
+ [原生計分../ scoring.md-原生 sql-），從 SQL Server 的快速批次預測，而不需要呼叫 R

本逐步解說提供計分使用批次和單一資料列模式中的預存程序的範例：

+ [中 SQL Server-結束資料科學逐步解說結束.../ tutorials/walkthrough-data-science-end-to-end-walkthrough.md）

請參閱這些解決方案範本，如需如何整合計分的應用程式中的範例：

+ [零售預測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [詐騙偵測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [群集的客戶](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

**提升效能和小數位數**


雖然已知開放原始碼 R 語言有限制，RevoScaleR 封裝 Api 可以處理大型資料集和受益於多執行緒、 多核心、 多處理序中的資料庫內部計算。

如果您的 R 解決方案使用複雜的彙總，或是牽涉到大型資料集，您可以利用 SQL Server 的高效率記憶體中彙總及資料行存放區索引，讓 R 程式碼處理統計計算和計分。

如需如何在 SQL Server 機器學習中改善效能的詳細資訊，請參閱：

+ [效能調整的 SQL Server R 服務../../ advanced-analytics/r/sql-server-r-services-performance-tuning.md）
+ [最佳化效能的秘訣和訣竅](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**調整其他平台的 R 程式碼，或計算內容**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-performance-for-r-services-results-and-resourcesrperformance-case-study-r-servicesmd"></a>5.&nbsp;[R 服務的效能： 結果和資源](r/performance-case-study-r-services.md)

*更新日期︰ 2017年-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 282.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 40c8cd255ead88edc60531d45dd0377ecbaf7c9b eeca5eed96e2223508910b246dbff18173eecea3  (PR=2565  ,  Filename=performance-case-study-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



RevoScaleR 和 MicrosoftML 封裝用來定型中複雜的 R 解決方案，牽涉到大型資料集的預測模型。 SQL 查詢和 R 程式碼完全相同。 所有測試所安裝的 SQL server 在單一 Azure VM 上都進行。 作者然後比較計分的時間，而不需要 SQL Server 提供的這些最佳化：

- 記憶體中資料表
- ssNoVersion
- 資源管理員

若要評估軟體 NUMA 的 R 指令碼執行的效果，資料科學團隊會測試在 Azure 虛擬機器與實體的 20 個核心方案。 四個軟體 NUMA 節點的每個節點包含五個核心的自動建立這些實體的核心上。

CPU 分配已強制在繼續比對案例中，以評估 R 作業的影響。 四個**SQL 資源集區**和第四個**外部資源集區**所建立，以確保組相同的 Cpu 可用於每個節點指定 CPU 相似性。

每個資源集區已指派給不同的工作負載群組，以最佳化的硬體使用率。 原因是軟體式 NUMA 和 CPU 相似性無法除以實體記憶體中實體的 NUMA 節點。因此，根據定義根據相同的實體 NUMA 節點的所有軟體 NUMA 節點必須使用記憶體中相同作業系統記憶體區塊。 換句話說，沒有無記憶體對處理器親和性。

下列程序用來建立此組態：

1. 減少至 SQL Server 預設配置的記憶體數量。

2. 建立四個新的集區以平行方式執行的 R 作業。

3. 因此，每個工作負載群組就會與資源集區相關聯，請建立四個工作負載群組。

4. 使用新的工作負載群組和指派，重新啟動資源管理員。

5. 建立使用者定義分類函數 (UDF)，來指派不同的工作負載群組中不同的工作。

6. 更新資源管理員組態，使用適當的工作負載群組的函數。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-performance-for-r-services---data-optimizationrr-and-data-optimization-r-servicesmd"></a>6.&nbsp;[R Services-資料最佳化的效能](r/r-and-data-optimization-r-services.md)

*更新日期︰ 2017年-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 107.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2ae2e54e8c5c8a3ec92fd2017088dd6ee879a9a1 9cb06bdce4ad6dfa2e9dc19da49103a6cd9817b3  (PR=2565  ,  Filename=r-and-data-optimization-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



> 如果資料來源，而不是查詢中指定的資料表，則 R 服務會使用內部的啟發學習法來判斷所需的資料行來擷取資料表;不過，這個方法不太可能會導致平行執行。

若要確保以平行方式，可分析資料，用來擷取資料的查詢應該包覆 database engine 可建立平行查詢計畫的方式。 如果程式碼或演算法使用的大量資料，請確定提供給查詢`RxSqlServerData`最適合用於平行執行。 不會導致平行執行計畫的查詢會導致單一處理序進行計算。

如果您要使用大型資料集，請使用 Management Studio 或另一個 SQL query analyzer 中的才能執行 R 程式碼，來分析執行計劃。 接著，採取任何建議的步驟，以改善查詢效能。 例如，資料表上遺漏的索引可能會影響執行查詢所花費的時間。 如需詳細資訊，請參閱 [監視和微調效能../../ relational-databases/performance/monitor-and-tune-for-performance.md）。

另一個常見的錯誤，可能會影響效能是查詢擷取多個資料行，比所需。 例如，如果公式根據只有三個資料行，但來源資料表有 30 的資料行，您會不必要地移動資料。

 + 請避免使用`SELECT *`！
 + 需要一些時間來檢閱資料集中的資料行，並識別分析所需的項目
 + 從您的查詢中移除包含的資料類型與 R 程式碼，例如 GUID 和 rowguids 的資料不相容的任何資料行
 + 不支援的日期和時間格式的檢查
 + 而不是載入資料表，請建立一個檢視，選取特定值或投射資料行，以避免發生轉換錯誤

**最佳化機器學習演算法**


本節提供其他的秘訣和 RevoScaleR 和 Microsoft R 中的其他選項特定的資源



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-r-package-management-for-sql-serverrr-package-management-for-sql-server-r-servicesmd"></a>7.&nbsp;[For SQL Server 的 R 封裝管理](r/r-package-management-for-sql-server-r-services.md)

*更新日期︰ 2017年-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 22.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2add5a7e1aef02487ac875e353c51161658050a4 5da92dd8b5402266a837172bda9aaabed3162ce8  (PR=2939  ,  Filename=r-package-management-for-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



本主題描述可用來管理 SQL Server 執行個體執行的 R 封裝的封裝管理功能。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

**使用 T-SQL 的封裝管理**


您可以繼續的電腦上，系統管理員身分安裝 R 封裝，如果您沒有這些權限，而且如果您是唯一的人使用機器學習工作的伺服器。

不過，如果您要與他人共用封裝，或有多人需要在伺服器上執行機器學習工作，它會更有效率，設定套件共用程式庫。 SQL Server 支援透過資料庫角色。

資料庫管理員負責設定角色，以及新增使用者至角色。 透過角色，資料庫管理員可以控制已加入或移除 SQL Server 環境中，R 封裝的權限的人員，以及可以稽核套件安裝。

**封裝管理的資料庫角色**


下列新的資料庫角色支援安全的安裝 R 封裝管理中與 SQL Server:

- `rpkgs-users`： 可讓使用者使用所安裝的成員的任何共用的封裝`rpkgs-shared`角色。

- `rpkgs-private`： 提供的相同權限與共用封裝的存取權`rpkgs-users`角色。 此角色成員也可以安裝、移除和使用具有私用範圍的封裝。

-  `rpkgs-shared`： 提供相同的權限`rpkgs-private`角色。 屬於此角色成員的使用者也可以安裝或移除共用封裝。

- `db_owner`： 具有相同的權限`rpkgs-shared`角色。 也可以授與使用者安裝或移除共用和私用封裝的權限。

**建立使用 T-SQL 的外部封裝程式庫**


此外，SQL Server 2017 支援 T-SQL 陳述式**建立外部程式庫**、 支援的資料庫管理員外部的程式庫的管理。 目前您可以使用此陳述式來建立 Windows 架構的程式庫 r 額外支援已規劃未來 Python 封裝和其他平台，例如 Linux 上執行寫入的封裝。



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>8.&nbsp;[設定 SQL Server 機器學習服務 （資料庫）](r/set-up-sql-server-r-services-in-database.md)

*更新日期︰ 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_7) | [下一步](#TitleNum_9))

<!-- Source markdown line 240.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 452dc36b4d0097f9562642238ba49eea0373d25b 4d355f6494b417dd90dce3943e7176eaece7336e  (PR=3070  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



如果您在資料科學用戶端電腦上建立 R 解決方案，而且需要使用 SQL Server 電腦當成計算內容中執行程式碼，您可以使用的 SQL 登入 」 或 「 整合式的 Windows 驗證。

* 針對 SQL 登入：確定此登入擁有您要讀取資料之資料庫的適當權限。 您可以藉由新增*連接到*和*選取*權限，或加入登入*db_datareader*角色。 針對要建立物件的登入、 新增*DDL_admin*權限。 登入，必須將資料儲存至資料表，請加入登入*db_datawriter*角色。

* Windows 驗證： 您可能需要在指定的執行個體名稱和其他連接資訊的資料科學用戶端上設定 ODBC 資料來源。 如需詳細資訊，請參閱[ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

**接下來的步驟**


SQL Server 中的指令碼執行功能，適用於在您確認之後，您可以執行 R 和 Python 命令從 SQL Server Management Studio、 Visual Studio 程式碼或任何其他用戶端，可以將 T-SQL 陳述式傳送到伺服器。

不過，您可能想要進行一些變更系統設定中，以支援大量使用機器學習服務，或將新的 R 封裝。

本節列出一些常見的修改，您可以對支援機器學習。

**新增更多背景工作帳戶**


如果您認為您可能會有很大，使用 R，或者您預期許多使用者會同時為執行指令碼，您可以增加背景工作帳戶指派給 Launchpad 服務數目。 如需詳細資訊，請參閱 [修改使用者帳戶集區的 SQL Server R Services--modify-the-user-account-pool-for-sql-server-r-services.md）。

**<a name="bkmk_optimize"></a>最佳化執行外部指令碼伺服器**




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-sql-server-configuration-for-use-with-rrsql-server-configuration-r-servicesmd"></a>9.&nbsp;[R 搭配使用的 SQL Server 組態](r/sql-server-configuration-r-services.md)

*更新日期︰ 2017年-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_8) | [下一步](#TitleNum_10))

<!-- Source markdown line 149.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3f57bae70e3c118c1e2bcd57017322940bae83f8 f296242d470db47077cba4215ef420bd0c60bf33  (PR=2660  ,  Filename=sql-server-configuration-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



如果查詢傳回單一記憶體節點 （節點 0），您沒有硬體 NUMA，或硬體設定為交錯的 (非 NUMA)。 SQL Server 也會忽略硬體 NUMA 時有四個或更少的 Cpu，或如果至少一個節點只有一個 CPU。

如果您的電腦有多個處理器，但沒有硬體 NUMA，您也可以使用[NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)至 Cpu 細分為較小的群組。  在 SQL Server 2016 和 SQL Server 2017，啟動 SQL Server 服務時，自動會啟用 NUMA 功能。

啟用 NUMA 時，SQL Server 自動節點會為您管理;不過，若要最佳化特定工作負載，您可以停用_軟性親和性_，然後手動設定軟體 NUMA 節點的 CPU 相似性。 這可讓您更多控制的工作負載指派給哪一個節點，特別是當您使用的支援支援資源監管的 SQL Server 版本。 指定 CPU 相似性，並對齊資源集區使用的 Cpu 群組，可以減少延遲，並確保相關處理序執行於相同的 NUMA 節點內。

設定軟體 NUMA 和 CPU 親和性來支援 R 工作負載的整體程序如下所示：

1. 如果有的話，請啟用軟體 NUMA
2. 定義處理器相關性
3. 建立資源集區外部處理序，使用 [資源管理員../r/resource-governance-for-r-services.md)
4. [工作負載群組...-指派/../ relational-databases/resource-governor/resource-governor-workload-group.md） 至特定的同質群組

如需詳細資訊，包括程式碼範例，請參閱本教學課程： [SQL 最佳化的秘訣和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他資源：**



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-performance-tuning-for-r-in-sql-serverrsql-server-r-services-performance-tuningmd"></a>10.&nbsp;[的 SQL Server 中的 R 效能微調](r/sql-server-r-services-performance-tuning.md)

*更新日期︰ 2017年-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_9) | [下一步](#TitleNum_11))

<!-- Source markdown line 76.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9c30753efdec81e499d5654b5b7a07f0cfe5b003 136a9f483bc8c9e1f69cf9d340d1472c21a52ec4  (PR=2565  ,  Filename=sql-server-r-services-performance-tuning.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



- 設定 SQL Server 執行個體，以平衡資料庫引擎作業，而 R 或 Python 指令碼在適當的層級的執行。 這可能包括變更 SQL Server 的記憶體和 CPU 使用量、 NUMA 和處理器親和性設定，以及建立資源群組的預設值。

- 最佳化伺服器電腦，以支援有效率地使用的外部指令碼。 這可以包括使用外部指令碼執行，請啟用封裝管理帳戶的數目增加，以及將使用者指派至相關的安全性角色。

- 將特定的最佳化套用至資料儲存和傳輸 SQL Server，包括索引和統計資料的策略，查詢設計及查詢最佳化資料表所使用的機器學習的設計。 您可能也會分析資料來源和資料傳輸方法，或是修改 ETL 處理序，以最佳化擷取特徵。

- 微調分析的模型，以避免無效率。 最佳化可能會有的範圍取決於您的 R 程式碼的封裝和您使用的資料的複雜性。 主要工作包括減少昂貴的資料轉換或卸載資料準備工作或功能工程工作從 R 或 Python ETL 處理序或 SQL。 您也可能重構指令碼、 消除內嵌封裝會安裝、 將 R 程式碼分割成不同的程序進行訓練、 計分，和評估，或簡化程式碼，以做為預存程序更有效率地運作。

**在這一系列的文章**


+ [在 SQL Server 硬體---微調效能..\r\sql-server-configuration-r-services.md)

    提供指導方針設定硬體，..！裡 NotShown-ssNoVersion_md...\..\includes\ssnoversion-md.md)]已安裝，而且可用於設定 SQL Server 執行個體，可更妥善支援外部指令碼。 它特別適用於**資料庫管理員**。

+ [效能微調 SQL Server 中的程式碼和資料最佳化..\r\r-and-data-optimization-r-services.md)



&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-data-science-scenarios-and-solution-templatestutorialsdata-science-scenarios-and-solution-templatesmd"></a>11.&nbsp;[資料科學案例和方案範本](tutorials/data-science-scenarios-and-solution-templates.md)

*更新日期︰ 2017年-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_10) | [下一步](#TitleNum_12))

<!-- Source markdown line 45.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 22c621731015f2192cb0b8d61b22062a4be50e70 6cf9e3f0a3803ed2bce9c4ffadfd7314f15f6b51  (PR=2964  ,  Filename=data-science-scenarios-and-solution-templates.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



[如何及何時預測潛在客戶的連絡](https://microsoft.github.io/r-server-campaign-optimization/)

**項目：**此解決方案使用保險業資料來預測潛在客戶根據人口統計資料、 歷程記錄的回應資料，以及特定產品的詳細資料。  表示最佳頻道與時間的方法來影響購買行為的使用者，也會產生建議。

**如何：**會建立方案，然後比較多個模型。 解決方案也會示範自動化的資料整合和資料準備使用預存程序。 SQL Server 資料庫內，在 Azure 和 HDInsight Spark 提供平行範例。

**健康照護： 預測醫院保持狀態的長度**


[醫院保持狀態的預測長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**項目：**準確地預測哪些病患可能需要長期住院是小心和計劃很重要的一部分。 系統管理員需要能夠判斷哪些功能需要更多資源，而且 caregivers 想要確保它們可以符合病患的需求。

**如何：**此解決方案使用 Data Science 虛擬機器，而且與啟用的機器學習中包含的 SQL Server 執行個體。 它也包含一組 Power BI 報表，您可以用來與已部署的模型互動。

**客戶變換**


[客戶變換預測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**項目：**分析和預測客戶變換量很重要，尤其必須管理及避免競爭對手客戶會遺失任何業界： 銀行、 電信和零售版，等等。 客戶流失分析的目標是為了識別哪些客戶可能流失，然後採取適當動作，以留下這類客戶並保持業務往來。



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-whats-new-in-machine-learning-services-in-sql-serverwhat-s-new-in-sql-server-machine-learning-servicesmd"></a>12.&nbsp;[的新功能 SQL Server 中的機器學習服務](what-s-new-in-sql-server-machine-learning-services.md)

*更新日期︰ 2017年-08-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_11))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025e68a93895a3788a63847cd91bff068775acf3 6dc0be2920c670235038a126d135e08d6f16ec3a  (PR=2712  ,  Filename=what-s-new-in-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=ea75391663eb4d509c10fb785fcf321558ff0b6e) -->



> 機器學習服務，包括使用 R 或 Python，目前不支援執行 SQL Server on Linux，或 Azure SQL 資料庫中時。 尋找下一個版本的變更。
>
> 不過，原生計分使用預測函數是目前支援的 Linux 版本。

**資料庫 Python 整合**


您可以在預存程序中執行 Python 或執行 Python 當成計算內容使用遠端 SQL Server 電腦。 這項整合會開啟新的 Python 開發人員及資料科學家使用的 SQL Server，以及以例如，microsoft 瀏覽創新 vast 社群途徑**revoscalepy**和**microsoftml**.

SQL Server 開發人員可以存取的更詳盡的 Python 程式庫的開放原始碼生態系統，包括熱門架構如 scikit-了解，Tensorflow、 Caffe 和 Theano/Keras。

但執行的 Python 資料庫中不是只為機器學習服務;有各種整合 Python SQL，利用個別的語言，以提供更智慧型、 功能強大的解決方案的優點與其他潛在的應用程式。

+ **revoscalepy**

    此版本包含的最終版本**revoscalepy**，其中提供資料流中 RevoScaleR 演算法的可擴充 Pythonic 對等項目。 您可以建立線性和羅吉斯迴歸、 決策樹，促進式樹狀結構，以及隨機樹系中，所有可並行，並且可以在遠端計算內容中執行 Python 模型。

    如需詳細資訊，請參閱 [revoscalepy-python/的模擬層是-revoscalepy.md 為何）。

+ Python 遠端計算內容

    此版本中支援多個資料來源和遠端計算內容使用。 資料科學家或開發人員可以執行遠端 SQL Server 上，瀏覽資料或建立模型，而不移動資料的 Python 程式碼。 使用遠端計算內容需要**revoscalepy**。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

此區段會列出最近已更新的發行項，在我們的公用 GitHub.com 儲存機制中的其他主體區域中的非常類似文件： [MicrosoftDocs/sql 的文件](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 12): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **Tools for SQL**文件](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **Master Data Services (MDS) sql**文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)



