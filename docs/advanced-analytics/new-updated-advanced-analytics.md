---
title: "更新-SQL Server 文件 Advanced Analytics |Microsoft 文件"
description: "顯示更新的內容，如需 Microsoft SQL server 的進階分析中最近變更過的文件的程式碼片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 02/03/2018
ms.openlocfilehash: a0c31eb21282cc876b34fc1c9d4b3e697f2c7213
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新增和更新最近： SQL Server 的進階分析



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017年-12-03** &nbsp; -到- &nbsp; **2018年-02-03**
- *主旨區域：* &nbsp; **Advanced Analytics for SQL Server**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


1. [在 SQL Server 上安裝新的 Python 套件](python/install-additional-python-packages-on-sql-server.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [機器學習服務中的已知的問題](#TitleNum_1)
2. [轉換執行資料庫內的 R 程式碼](#TitleNum_2)
3. [判斷 SQL Server 上已安裝的 R 封裝](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1.&nbsp;[機器學習服務中的已知問題](known-issues-for-sql-server-machine-learning-services.md)

*更新日期︰ 2018年-02-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 163.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c6f46adcf795c43f818120b88407a3a89304cb27 c781562605f5cd77f6c43bfe5e89810cb72ceae0  (PR=4789  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=386bfb688843bac7fa4d83dc1cfef94dd19db110) -->



如需其他可能會影響 R 解決方案的已知問題，請參閱[Server 機器學習](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站台。

**在非預設位置的 SQL Server 上執行 R 指令碼時存取被拒警告**


如果 SQL Server 執行個體已安裝到非預設位置，例如外部`Program Files`資料夾中，當您嘗試執行安裝套件的指令碼時，會引發 ACCESS_DENIED 警告。 例如：

> *In normalizePath(path.expand(path), winslash, mustWork) : path[2]="~ExternalLibraries/R/8/1": Access is denied*

R 函式會嘗試讀取此路徑，而如果會失敗，原因是內建使用者群組**SQLRUserGroup**，並沒有讀取權限。 就會引發此警告不會封鎖執行目前的 R 指令碼，但警告可能會重複發生，每當使用者執行任何其他的 R 指令碼。

如果您已安裝 SQL Server 的預設位置，這不會發生錯誤，因為所有的 Windows 使用者擁有讀取權限`Program Files`資料夾。

在服務即將發行版本中，將會解決這個問題。 因應措施，提供群組， **SQLRUserGroup**，具有讀取存取權的所有父資料夾`ExternalLibraries`。

**舊的和新版本之間的 RevoScaleR 序列化錯誤**


當您將使用遠端 SQL Server 執行個體的序列化的格式的模型時，您可能會收到錯誤：

> *MemDecompress 時發生錯誤 (資料、 類型 = 解壓縮) 發生內部錯誤-3 memDecompress(2)。*

如果您儲存使用的序列化函式中，新版本的模型，會引發這個錯誤[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，但您還原序列化模型的 SQL Server 執行個體有較舊版本的 RevoScaleR Api，從 SQLServer 2017 CU2 或更早版本。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-converting-r-code-for-execution-in-databaserconverting-r-code-for-use-in-sql-servermd"></a>2.&nbsp;[轉換 R 程式碼的執行中的資料庫](r/converting-r-code-for-use-in-sql-server.md)

*更新日期︰ 2018年-01-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 136.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a1d156fac1af5813ef75965071686b177e2aede7 fc8beff0aa0d7ea298e493b90984875e81e9143e  (PR=4493  ,  Filename=converting-r-code-for-use-in-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f486d12078a45c87b0fcf52270b904ca7b0c7fc8) -->



**封裝的預存程序中的 R 程式碼**

+ 如果您的程式碼相當簡單，您可以將它內嵌在 T-SQL 使用者自訂函數不需修改這些範例中所述：

    + [建立會在 rxExec 中執行的 R 函數](r/../tutorials/deepdive-create-a-simple-simulation.md)
    + [使用 T-SQL 和 R 功能工程](r/../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 如果程式碼更複雜，請使用 R 封裝**sqlrutils**轉換您的程式碼。 此封裝被為了幫助經驗豐富的 R 使用者撰寫好預存程序程式碼。

    第一個步驟是將 R 程式碼改寫具有明確定義的輸入和輸出的單一函式。

    然後，使用**sqlrutils**產生格式正確的輸入和輸出的封裝。 **Sqlrutils**封裝產生完整的預存程序程式碼，和也在資料庫中註冊預存程序。

    如需詳細資訊和範例，請參閱[SqlRUtils](r/../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。

**與其他工作流程整合**

+ 利用 T-SQL 的工具和 ETL 程序。 執行特徵設計、 擷取特徵，以及資料清理事先做為資料工作流程的一部分。

    當您正在 Visual Studio 或 RStudio 專用 R 開發環境，例如 R 工具中時，您可能資料提取到您的電腦、 反覆，分析資料然後寫出或顯示結果。

    不過，當您獨立 R 程式碼移轉至 SQL Server，此程序的許多簡化或委派給其他 SQL Server 工具。

+ 使用安全且非同步的視覺效果的策略。

    SQL Server 的使用者通常無法存取伺服器上的檔案和 SQL 用戶端工具通常不支援 R 圖形裝置。 如果您產生繪圖或其他圖形做為方案的一部分，請考慮將圖匯出為二進位資料並儲存至資料表，或寫入。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3.&nbsp;[判斷 SQL Server 上已安裝的 R 封裝](r/determine-which-packages-are-installed-on-sql-server.md)

*更新日期︰ 2018年-01-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2))

<!-- Source markdown line 78.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9a065066398843a4bed318fa46d4982d712915a9 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f  (PR=4715  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=9e6a029456f4a8daddb396bc45d7874a43a47b45) -->




**取得程式庫位置和版本**


下列範例會取得在本機計算內容和封裝版本的 RevoScaleR 文件庫位置。

```
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

**判斷 SQL Server 所使用的程式庫路徑**


如果您已升級的機器學習使用繫結元件，可能會變更的 R 程式庫的路徑。 當發生這種情況時，R 工具的上一個捷徑可能會參考先前的版本。 為了確保的 SQL Server 所使用的路徑及封裝版本，您可以執行的命令如下所示：

```
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**結果**

```
STDOUT message(s) from external script:
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```







## <a name="similar-articles-about-new-or-updated-articles"></a>新的或更新的發行項相關的類似文件

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主旨區域，*不要*new 或最近更新發行項


- [新 + 更新 (1 + 3):&nbsp; **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (0 + 1):&nbsp; **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 1):&nbsp; **連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1):&nbsp; **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (12 + 1): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (6 + 2):&nbsp; **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (15 + 0):**適用於 SQL PowerShell**文件](../powershell/new-updated-powershell.md)
- [新 + 更新 (2 + 9):&nbsp; **關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (1 + 0):&nbsp; **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 1):&nbsp; **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (1 + 1):&nbsp; **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)**文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)**文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2):&nbsp; **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主旨區域執行*不*有任何新的或最近的更新發行項


- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX Data Objects (ADO) 的 SQL**文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (0 + 0): **SQL 的 Data Quality Services**文件](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**資料採礦延伸模組 (DMX)，sql**文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多維度運算式 (MDX) 的 SQL**文件](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **ODBC （開放式資料庫連接） 的 SQL**文件](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**範例 sql**文件](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **sql XQuery**文件](../xquery/new-updated-xquery.md)


