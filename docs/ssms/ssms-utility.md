---
description: SSMS 公用程式
title: SSMS 公用程式
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/24/2020
ms.openlocfilehash: 4cc43babe2ae064731f293a0dc96219aaeced5a5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035993"
---
# <a name="ssms-utility"></a>SSMS 公用程式

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**SSMS** 公用程式會開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 如果有指定， **Ssms** 也會建立伺服器的連接，且會開啟查詢、指令碼、檔案、專案和方案。

您可以指定包含查詢、專案或方案的檔案。 如果提供了連接資訊，且檔案類型與這個類型的伺服器相關聯，包含查詢的檔案會自動連接伺服器。 例如，.sql 檔案會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟一個 [SQL 查詢編輯器] 視窗，.mdx 檔案則會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟一個 [MDX 查詢編輯器] 視窗。 而 **SQL Server 解決方案和專案** 則會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟。

> [!NOTE]
> **Ssms** 公用程式不會執行查詢。 若要從命令列中執行查詢，請使用 **sqlcmd** 公用程式。 

## <a name="syntax"></a>語法

```syntaxsql
Ssms
[scriptfile] [projectfile] [solutionfile] 
[-S servername] [-d databasename] [-G] [-U username] [-E] [-nosplash] [-log [filename]?] [-?] 
```

## <a name="arguments"></a>引數

*scriptfile* 指定一個或多個要開啟的指令碼檔案。 這個參數必須包含檔案的完整路徑。 

*projectfile* 指定要開啟的指令碼專案。 這個參數必須包含指令碼專案檔的完整路徑。 

*solutionfile* 指定要開啟的解決方案。 這個參數必須包含方案檔的完整路徑。 

[ **-S** _servername_] 伺服器名稱

[ **-d** _databasename_] 資料庫名稱

[ **-G**] 使用 Active Directory 驗證來連線。 是否包含 **-U** 會決定連線的類型。

> [!Note]
> 目前不支援**具 MFA 支援的 Active Directory - 通用**。

[ **-U** _username_] 與「SQL 驗證」連線時的使用者名稱

> [!Note]
> SSMS 18.0 版已移除 **-P**。
>
> 因應措施：嘗試使用 UI 連線到伺服器一次，並儲存密碼。

[ **-E**] 使用 Windows 驗證進行連線

[ **-nosplash**] 在開啟時，避免 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 出現在啟動顯示畫面圖形中。 當您利用頻寬有限的連接，透過「終端機服務」來連接執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的電腦時，請使用這個選項。 這個引數不區分大小寫，可出現在其他引數的前後。

[ **-log** _[檔案名稱]?_ ] 將 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 活動記錄到指定的檔案，以利於疑難排解

[ **-?** ] 顯示命令列說明

## <a name="remarks"></a>備註

所有參數皆為選擇性參數，以空格加以分隔，但檔案除外，檔案以逗號分隔。 如果您沒有指定任何參數，**Ssms** 會依照 [工具] 功能表上，[選項] 設定中所指定的內容來開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 例如，如果 [環境/一般] 頁面的 [啟動時] 選項指定了 [開啟新增查詢視窗]，**Ssms** 開啟時就會出現空白的查詢編輯器。

**-log** 參數必須出現在命令列結尾，位於所有其他參數之後。 檔名引數是選擇性的。 如果指定了檔名，但該檔案不存在，便會建立檔案。 若因寫入權限不足等緣故而無法建立檔案，則會改將記錄寫入未當地語系化的 APPDATA 位置 (請參閱下文)。 如果未指定檔名引數，便會將兩個檔案寫入至目前使用者的未當地語系化應用程式儲存資料夾。 SQL Server 的未當地語系化應用程式儲存資料夾可以由 APPDATA 環境變數查知。 例如，SQL Server 2012 的資料夾是 \<system drive>:\Users\\<使用者名稱\>\AppData\Roaming\Microsoft\AppEnv\10.0\\。 兩個檔案依預設將名為 ActivityLog.xml 和 ActivityLog.xsl。 前者包含活動記錄資料，後者則是 XML 樣式表，供您更方便檢視此 XML 檔案。 請使用下列步驟，在您的預設 XML 檢視器 (如 Internet Explorer) 中檢視記錄檔：依序按一下 [開始] 和 [執行...]，然後在提供的欄位內鍵入 "\<system drive>:\Users\\<使用者名稱\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml"，然後按 Enter。

如果提供了連線資訊，且檔案類型與這類伺服器相關聯，便會對包含查詢的檔案發出會連線到伺服器的提示。 例如，.sql 檔案會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟一個 [SQL 查詢編輯器] 視窗，.mdx 檔案則會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟一個 [MDX 查詢編輯器] 視窗。 而 **SQL Server 解決方案和專案** 則會在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟。

下表將伺服器類型對應至副檔名。

| 伺服器類型 | 分機 |
|-------------|-----------|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|
|SQL Server Analysis Services|.mdx<br /><br /> .xmla|

## <a name="examples"></a>範例

下列指令碼會在命令提示字元之下，利用預設值來開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ：

```console
  Ssms
```

下列指令碼會使用 *Active Directory - 整合*，從命令提示字元開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]：

```console
Ssms.exe -S servername.database.windows.net -G
```

下列指令碼會在命令提示字元之下，將程式碼編輯器設為伺服器 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，在不呈現開頭顯示畫面的情況下，利用 Windows 驗證來開啟 `ACCTG and the database AdventureWorks2012,` ：

```console
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash
```

下列指令碼會在命令提示字元之下開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，且會開啟 MonthEndQuery 指令碼。

```console
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"
```

下列指令碼會在命令提示字元之下開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，且會在名稱為 `developer`的電腦上開啟 NewReportsProject 專案：

```console
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"
```

下列指令碼會在命令提示字元之下開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，且會開啟 MonthlyReports 方案： 

```console
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"
```

## <a name="see-also"></a>另請參閱

[使用 SQL Server Management Studio](./sql-server-management-studio-ssms.md)