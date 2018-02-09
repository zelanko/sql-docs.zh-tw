---
title: "已更新-SQL Server on Linux 的文件 |Microsoft 文件"
description: "顯示更新的內容，如需 Microsoft SQL Server on Linux 的最近變更過的文件的程式碼片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: linux
ms.date: 02/03/2018
ms.openlocfilehash: fc740b59397f0438a059b38df57ffc40999cc81e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的與最近的更新： SQL Server on Linux 的文件



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017年-12-03** &nbsp; -到- &nbsp; **2018年-02-03**
- *主旨區域：* &nbsp; **Microsoft SQL Server on Linux**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


1. [設定多重子網路 Alwayson 可用性群組和容錯移轉叢集執行個體](sql-server-linux-configure-multiple-subnet.md)
2. [建立及設定可用性群組的 SQL Server on Linux](sql-server-linux-create-availability-group.md)
3. [Pacemaker 叢集部署的 SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md)
4. [SQL Server on Linux 常見問題集 (FAQ)](sql-server-linux-faq.md)
5. [Linux 部署的 SQL Server 可用性基本概念](sql-server-linux-ha-basics.md)
6. [SQL Server 容器 Kubernetes 中設定高可用性](tutorial-sql-server-containers-kubernetes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [Always On Linux 上的可用性群組](#TitleNum_1)
2. [擷取、 轉換和載入與 SSIS Linux 上的資料](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-always-on-availability-groups-on-linuxsql-server-linux-availability-group-overviewmd"></a>1.&nbsp;[Always On Linux 上的可用性群組](sql-server-linux-availability-group-overview.md)

*更新日期︰ 2018年-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 85.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 85685bc8ad3528aa26ca3f2bba7b0112808ad6f9 51aff6e55104c8f775d2b4f4461e44f689a9ee6b  (PR=4768  ,  Filename=sql-server-linux-availability-group-overview.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



符合下列條件時，就可能的 AG 的自動容錯移轉：

-   主要和次要複本設定為同步的資料移動。
-   次要資料庫都有同步處理 （未進行同步處理），表示兩個在相同的資料點的狀態。
-   叢集類型設定為外部。 自動容錯移轉不可能叢集類型為 None。
-   `sequence_number`變成次要複本的主要具有最高的序號-亦即，次要複本的`sequence_number`符合從原始的主要複本。

如果符合這些條件，而裝載主要複本的伺服器失敗，AG 會變成同步複本的擁有權。 同步複本的行為 (其中可以有三個的總計： 一個主要和兩個次要複本) 可以進一步控制`required_synchronized_secondaries_to_commit`。 這適用於 Windows 和 Linux 上 Ag，但設定完全不同。 On Linux，值會自動根據本身的 AG 資源上的叢集設定。

**設定唯讀複本和仲裁**


新 SQL Server 2017 年 CU1 中也設定唯讀複本。 因為 Pacemaker 不同 WSFC，尤其是當談到仲裁和需要 STONITH，只要雙節點設定設定無法運作時 AG。 使用 fci，Pacemaker 所提供的仲裁機制可能沒問題，因為所有的 FCI 容錯移轉仲裁會發生在叢集的圖層。 AG，對於 Linux 底下的仲裁會進行中的所有中繼資料儲存所在的 SQL Server。 這是設定唯讀複本會發揮作用。

沒有任何其他項目，第三個節點和至少一個同步處理的複本將會是必要。 這不適用於 SQL Server Standard，因為它可以只包含兩個複本 AG 中的參與。 設定唯讀複本會儲存在 master 資料庫中，AG 組態中的其他複本相同 AG 組態。 設定唯讀複本沒有參與 AG 中的使用者資料庫。 設定資料是從主要以同步方式傳送。 此設定資料則會使用容錯移轉期間，無論是自動或手動。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-extract-transform-and-load-data-on-linux-with-ssissql-server-linux-migrate-ssismd"></a>2.&nbsp;[擷取、 轉換及載入資料，SSIS 與 Linux 上](sql-server-linux-migrate-ssis.md)

*更新日期︰ 2018年-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1))

<!-- Source markdown line 50.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9bba002ae3955ebb8376c7c85b7ec1ac8c706073 1533a8e0bfe553e5404de79129119b3f93185ee9  (PR=4768  ,  Filename=sql-server-linux-migrate-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  指定`/de[crypt]`選項，即可輸入密碼，以互動方式如下列範例所示：

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de

    Enter decryption password:
    ```

3.  指定`/de`命令列上提供的密碼，如下列範例所示的選項。 不建議這個方法，因為它會使用命令的解密密碼儲存在 命令歷程記錄中。

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test

    Warning: Using /De[crypt] <password> may store decryption password in command history.

    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

**設計封裝**


**連接至 ODBC 資料來源**。 在重新整理 Linux CTP 2.1 和更新版本的 SSIS，SSIS 封裝可以使用 ODBC 連接 on Linux。 這項功能經過測試可與 SQL Server 及 MySQL ODBC 驅動程式，但也應該使用 ODBC 規格會觀察到的任何 Unicode ODBC 驅動程式。 在設計階段，您可以提供 DSN 或連接字串連接至 ODBC 資料;您也可以使用 Windows 驗證。 如需詳細資訊，請參閱[部落格文章發表的 ODBC 支援在 Linux 上](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。







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


