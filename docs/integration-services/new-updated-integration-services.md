---
title: "已更新 - Integration Services for SQL Server 文件 | Microsoft Docs"
description: "針對 Integration Services for Microsoft SQL Server，顯示文件最新變更之已更新內容的程式碼片段。"
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
ms.workload: integration-services
ms.openlocfilehash: 9660fa7239c14c3adc963cc75ceb98de8316734c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>新增和最近更新：Integration Services for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp; **2017-09-28** &nbsp; 到 &nbsp; **2017-12-02**
- *主旨區域：*&nbsp;**Integration Services for SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [使用 SSIS 來儲存與擷取內部部署和 Azure 中檔案共用上的檔案](lift-shift/ssis-azure-files-file-shares.md)
2. [驗證部署到 Azure 的 SSIS 套件](lift-shift/ssis-azure-validate-packages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [Hadoop 連線管理員](#TitleNum_1)
2. [使用 Windows 驗證來連線至內部部署資料來源和 Azure 檔案共用](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-hadoop-connection-managerconnection-managerhadoop-connection-managermd"></a>1.&nbsp; [Hadoop 連線管理員](connection-manager/hadoop-connection-manager.md)

*更新日期：2017-11-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 65.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2d68f4e884304f1a28045b42b680c15cc6a41ec5 fb2429466ea4d545682975d8dbea47451ce98ec7  (PR=4113  ,  Filename=hadoop-connection-manager.md  ,  Dirpath=docs\integration-services\connection-manager\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



**使用 Kerberos 驗證進行連線**

有兩個選項可設定內部部署環境，以便讓您使用 Hadoop 連線管理員搭配 Kerberos 驗證。 您可以選擇較適合您情況的選項。
-   選項 1：[將 SSIS 電腦加入 Kerberos 領域--#kerberos-join-realm)
-   選項 2：[啟用 Windows 網域和 Kerberos 領域之間的相互信任--#kerberos-mutual-trust)

**<a name="kerberos-join-realm"></a>選項 1：將 SSIS 電腦加入 Kerberos 領域**


**需求：**


-   閘道電腦必須加入 Kerberos 領域，且無法再加入任何 Windows 網域。

**如何設定：**


**在 SSIS 電腦上：**

1.  執行 **Ksetup** 公用程式來設定 Kerberos KDC 伺服器和領域。

    電腦必須設定為工作群組成員，因為 Kerberos 領域與 Windows 網域不同。 如下列範例中所示，設定 Kerberos 領域並新增 KDC 伺服器。 視需要使用您的領域來取代 *REALM.COM*。

```
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
```

    Restart the computer after executing these two commands.

2.  使用 **Ksetup** 命令來確認設定。 輸出看起來應該像下列範例：

```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
```

**<a name="kerberos-mutual-trust"></a>選項 2：啟用 Windows 網域和 Kerberos 領域之間的相互信任**


**需求：**

-   閘道電腦必須加入 Windows 網域。
-   您需要更新網域控制站設定的權限。

**如何設定：**


> [!NOTE]
> 在下列教學課程中，視需要使用您的領域和網域控制站來取代 REALM.COM 和 AD.COM。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authenticationlift-shiftssis-azure-connect-with-windows-authmd"></a>2.&nbsp; [使用 Windows 驗證來連線至內部部署資料來源和 Azure 檔案共用](lift-shift/ssis-azure-connect-with-windows-auth.md)

*更新日期：2017-11-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 66.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 673386fca53cb60b983e0cb3cd4b9e2ee1dee0de 65458b4dceb92d01184c5e9c6f68ec0e8f16ba08  (PR=4104  ,  Filename=ssis-azure-connect-with-windows-auth.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=19e1c4067142d33e8485cb903a7a9beb7d894015) -->



**連線到內部部署 SQL Server**

若要檢查是否可以連線至內部部署 SQL Server，請執行下列動作：

1.  若要執行這項測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令，以您想要使用的網域認證啟動 SQL Server Management Studio (SSMS)：

```
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
```

3.  從 SSMS 中，檢查是否可以連線至您想要使用的內部部署 SQL Server。

**連線至內部部署檔案共用**

若要檢查是否可以連線至內部部署檔案共用，請執行下列動作：

1.  若要執行這項測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令。 此命令會使用您要使用的網域認證開啟命令提示字元視窗，然後藉由取得目錄清單來測試與檔案共用的連線。

```
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
```

3.  檢查是否會針對您要使用的內部部署檔案共用傳回目錄清單。

**連線至 Azure VM 上的檔案共用**

若要連線到 Azure 虛擬機器上的檔案共用，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行 `catalog.set_execution_credential` 預存程序，如下列選項中所述：

```
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
```

**連線至 Azure 檔案中的檔案共用**

如需 Azure 檔案的詳細資訊，請參閱 [Azure 檔案](https://azure.microsoft.com/services/storage/files/)。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (3+14)：**SQL 的進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (87+0)：**SQL 的分析平台系統**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (5+4)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：**SQL 的資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (2+2)：**SQL 的 Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (10+9)：**SQL 適用的 Linux** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (2+4)：**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (4+2)：**SQL 的 Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+1)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (21+0)：**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (5+1)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


