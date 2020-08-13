---
title: 舊版的 SQL Server Data Tools (SSDT)
description: 了解哪些版本的 SSDT 及 SSDT-BI 可與哪些版本的 Visual Studio 搭配使用。 請參閱如何安裝不同版本的 SSDT 及 SSDT-BI。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 06/17/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: f6fea0264cdbd28c8f6665f5f0d67eda4a8da3c9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009948"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>舊版的 SQL Server Data Tools (SSDT 和 SSDT-BI)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL Server Data Tools (SSDT) 提供專案範本及設計介面以建置 SQL Server 內容類型，包括關聯式資料庫、Analysis Services 模型、Reporting Services 報表及 Integration Services 套件。

SSDT 可以回溯相容，亦即您可以隨時使用[最新的 SSDT](download-sql-server-data-tools-ssdt.md) 設計及部署要在舊版 SQL Server 上執行的資料庫、模型、報表及套件。

過去會使用 Visual Studio Shell 來建立已用其他各種名稱發行的 SQL Server 內容類型，包括 **SQL Server Data Tools**、 **SQL Server Data Tools - Business Intelligence**以及 **Business Intelligence Development Studio**。 舊版隨附不同的專案範本集。 若要在一個 SSDT 中取得所有專案範本，您需要使用 [最新版本](download-sql-server-data-tools-ssdt.md)。 否則，您可能會需要安裝多個舊版本才能取得 SQL Server 中使用的所有範本。 每個 Visual Studio 版本只會安裝一個 Shell；安裝第二個 SSDT 只會新增缺少的範本。

## <a name="previous-ssdt-releases"></a>舊版 SSDT

選取相關區段中的下載連結，以下載舊版的 SSDT。

| SSDT 版本 | Visual Studio 版本 |
|--------------|-----------------------|
| [15.8](#ssdt-for-visual-studio-vs-2017) | 2017 |
| [17.4](#ssdt-for-visual-studio-vs-2015) | 2015 |
| [16.5](#ssdt-for-visual-studio-vs-2013) | 2013 |
| [11.1.50727.1](#ssdt-for-visual-studio-vs-2012) | 2012 |

### <a name="ssdt-for-visual-studio-vs-2017"></a>適用於 Visual Studio (VS) 2017 的 SSDT

**[下載適用於 Visual Studio 2017 的 SSDT (15.8)](https://go.microsoft.com/fwlink/?linkid=2124319)**

此**適用於 Visual Studio 2017 的 SSDT** 版本可安裝於下列語言版本：

[簡體中文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40a)

### <a name="ssdt-for-visual-studio-vs-2015"></a>適用於 Visual Studio (VS) 2015 的 SSDT

若要安裝此 SSDT 版本，則必須下載 ISO 映像。 ISO 檔案是一個獨立的檔案，其內含 SSDT 需要的所有元件，且可使用隨時啟動下載管理員來下載，而且非常適合在網路頻寬有限或不穩時使用。 下載後，ISO 可掛載為磁碟機。

安裝步驟：

1. **[下載適用於 Visual Studio 2015 的 SSDT (17.4)](https://go.microsoft.com/fwlink/?linkid=2132817)** 。

2. 開啟 ISO 映像。

3. 執行 *SSDTSetup.exe* 檔案。

    ![ISO 映像檔](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

此 **適用於 Visual Studio 2015 的 SSDT** 版本可安裝於下列語言版本：

| Language | SHA256 雜湊 |
|----------|-------------|
| [簡體中文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [繁體中文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [法文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [德文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [義大利文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [日文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [韓文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [俄文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [西班牙文](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2013"></a>適用於 Visual Studio (VS) 2013 的 SSDT

若要安裝此 SSDT 版本，則必須下載 ISO 映像。 ISO 檔案是一個獨立的檔案，其內含 SSDT 需要的所有元件，且可使用隨時啟動下載管理員來下載，而且非常適合在網路頻寬有限或不穩時使用。 下載後，ISO 可掛載為磁碟機。

安裝步驟：

1. **[下載適用於 Visual Studio 2013 的 SSDT (16.5)](https://go.microsoft.com/fwlink/?linkid=832312)**

2. 開啟 ISO 映像。

3. 執行 *SSDTSetup.exe* 檔案。

    ![ISO 映像檔](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

此 **適用於 Visual Studio 2013 的 SSDT** 版本可安裝於下列語言版本：

| Language | SHA256 雜湊 |
|----------|-------------|
| [簡體中文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [繁體中文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [法文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [德文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [義大利文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [日文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [韓文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [俄文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [西班牙文](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2012"></a>適用於 Visual Studio (VS) 2012 的 SSDT

若要安裝此 SSDT 版本，則必須下載 ISO 映像。 ISO 檔案是一個獨立的檔案，其內含 SSDT 需要的所有元件，且可使用隨時啟動下載管理員來下載，而且非常適合在網路頻寬有限或不穩時使用。 下載後，ISO 可掛載為磁碟機。

安裝步驟：

1. **[下載適用於 Visual Studio 2012 的 SSDT (11.1.50727.1)](https://go.microsoft.com/fwlink/?linkid=518814)**

2. 開啟 ISO 映像。

3. 執行 *SSDTSetup.exe* 檔案。

    ![ISO 映像檔](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

此 **適用於 Visual Studio 2012 的 SSDT** 版本可安裝於下列語言版本：

| Language | SHA256 雜湊 |
|----------|-------------|
| [簡體中文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x804) | 78F20325648CFF49D9C58A26186E0AC199D104B3CF634E5663B4B262BEC69C07 |
| [繁體中文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x404) | A2722380AF2EE1E8BB52B4FA54A61BAB411E5E5FD5B050108F81ED23DC87366D |
| [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x409) | 748EF78D3F9CC6FE360432C378EA690DE51AEB2C747E87D43E08448D26F93A91 |
| [法文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40c) | 40E6504169BF618EDC7EB5B62D1215DC96726D6EEC3CA8EC3EEB49044E4B6FB7 |
| [德文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x407) | C45C974E6B8F9611BA2AC1EE90C5C507992BCE5693BF46F6C7C138591ED6A123 |
| [義大利文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x410) | C1B20CDB41C7B1B5DE76A71F9A091A6FDF5186B12F6AA269DA6338B3CB2D91A6 |
| [日文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x411) | BF56958B904C1C5F28084BD0B16928B6CBFEC83EB3F0C913EC364FA335241943 |
| [韓文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x412) | 9023B0656785C357A67E39EB76A2806B923C2BD17342D7226A8ADA384A9F4E28 |
| [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x416) | ACAD9FE03729E289ECE821D92C56CFB1D7FCCEA8423ABF1E164BF3C67ABEFEFB |
| [俄文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x419) | E2191D787BA833DF4A85B064C5373DC44099E76214FBF9505728702D4D6B83F0 |
| [西班牙文](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40a) | 6D81FB572A7003C54C29D2ACF076D2CED4A1CA80F329BFF9D41A806920D64EEE |

> [!Note]
> SSDT 支援兩個最新版的 Visual Studio。 隨著 Visual Studio 2019 的發行，適用於 Visual Studio 2015 及較舊版本的 SSDT 版本將不再更新。 使用於 Visual Studio 2010 的 SSDT 將不再使用。 如需詳細資訊，請參閱[這篇 SSDT 小組部落格文章](https://blogs.msdn.microsoft.com/ssdt/2017/03/10/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017/)的＜常見問題集＞一節。

## <a name="sql-bi-analysis-services-reporting-services-integration-services"></a>SQL BI：Analysis Services、Reporting Services、Integration Services

BI 範本用來建立 SSAS 模型、SSRS 報表及 SSIS 套件。 BI 設計工具與特定版本的 SQL Server 一併發行。 要使用較新的 BI 功能，請安裝較新版本的設計工具。

## <a name="bi-designers"></a>BI 設計工具

[下載 SSDT-BI for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313) (SQL Server 2014、SQL Server 2012、SQL Server 2008 和 2008 R2)

[下載 SSDT-BI for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843) (SQL Server 2014、SQL Server 2012、SQL Server 2008 和 2008 R2)

Business Intelligence Development Studio (BIDS) 是透過 SQL Server 安裝程式安裝。 沒有網站下載 (SQL Server 2008 與 2008 R2)。

對於 SQL Server 2012 或 2014，您可以使用 **適用於 Visual Studio 2012 的 SSDT-BI** 或 **SSDT-BI f或 Visual Studio 2013**。 這兩者的唯一差異是 Visual Studio 版本的不同。

## <a name="next-steps"></a>後續步驟

- [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [SQL Server Data Tools (SSDT) 版本資訊](release-notes-ssdt.md)
- [下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- [下載 Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)
- [SQL 工具和公用程式](../tools/overview-sql-tools.md)