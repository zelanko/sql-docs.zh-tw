---
title: '[產生和發佈指令碼]'
description: 了解如何使用 [產生和發佈指令碼精靈] 建立指令碼，以在資料庫執行個體之間傳送資料庫。 執行個體可以是 SQL Server 資料庫引擎或 Azure SQL Database 的執行個體。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql13.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql13.swb.generatescriptswizard.summarypage.f1
- sql13.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql13.swb.generatescriptswizard.introduction.f1
- sql13.swb.generatescriptswizard.setscriptingoptions.f1
- sql13.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql13.swb.generatescriptswizard.chooseobjects.f1
- sql13.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.choosetables.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql13.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 04/07/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edbce6b52c224bc95aad1b3a6088696dba4c4f6a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039015"
---
# <a name="generate-and-publish-scripts-wizard"></a>[產生和發佈指令碼]

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

您可以使用 [產生和發佈指令碼精靈]  建立指令碼，以在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 執行個體之間傳送資料庫。 您可以針對區域網路上 Database Engine 執行個體的資料庫產生指令碼，或是從 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]產生指令碼。 產生的指令碼可以在另一個 Database Engine 或 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]執行個體上執行。 您也可以使用此精靈，將資料庫內容直接發行到使用資料庫發行服務所建立的 Web 服務。 您可以針對整個資料庫建立指令碼，或將它限制為特定物件。

如需使用 [產生和發佈指令碼精靈] 的更詳細教學課程，請參閱[教學課程：產生指令碼精靈](../tutorials/scripting-ssms.md#script-databases)。

## <a name="before-you-begin"></a>開始之前

來源和目標資料庫可以位於執行 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或更新版本的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體上。

### <a name="publishing-to-a-hosted-service"></a><a name="PubHostSvc"></a> 發行至主控的服務

除了建立指令碼以外， **[產生和發佈指令碼精靈]** 還可以用來將資料庫發佈至特定類型的主控 SQL Server Web 服務。 SQL Server Hosting Toolkit 會提供資料庫發行服務當做 CodePlex 上的共用原始檔專案。 Web 主控提供者可以使用資料庫發行服務專案來建置一組 Web 服務，讓他們的客戶輕鬆地將資料庫部署到 Web 服務。 如需有關下載 SQL Server Hosting Toolkit 的詳細資訊，請參閱 [SQL Server 資料庫發行服務](https://go.microsoft.com/fwlink/?LinkId=142025)。

若要將資料庫發佈至 Web 主控服務，請選取精靈之 **[設定指令碼編寫選項]** 頁面上的 **[發佈到 Web 服務]** 選項。

### <a name="permissions"></a><a name="Permissions"></a> 權限

發行資料庫的最低權限是來源資料庫上 db_ddladmin 固定資料庫角色中的成員資格。 將資料庫指令碼發行至位於主控提供者之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的最低權限是目標資料庫上 db_ddladmin 固定資料庫角色中的成員資格。

此外，使用者也必須提供使用者名稱和密碼來存取主控提供者帳戶，以便使用此精靈發行。 您必須先在主控提供者處建立目標資料庫，然後再發行來源資料庫。 發行會覆寫現有資料庫中的物件。

## <a name="using-the-generate-and-publish-scripts-wizard"></a><a name="GenPubScriptWiz"></a> 使用產生和發佈指令碼精靈

**產生和發佈指令碼**

1. 在 **[物件總管]** 中，展開含有要編寫指令碼之資料庫的執行個體的節點。

2. 指向 [工作]  ，然後選取 [產生指令碼]  。

    ![產生指令碼精靈](media/generate-and-publish-scripts-wizard/generate-scripts.png)

3. 完成精靈對話方塊：

    - [簡介頁面](#Introduction)
    - [選擇物件頁面](#ChooseObjects)
    - [設定指令碼編寫選項頁面](#SetScriptOpt)
    - [進階編寫指令碼選項頁面](#AdvScriptOpt)
    - [摘要頁面](#Summary)
    - [儲存或發佈指令碼頁面](#SavePubScripts)

###  <a name="introduction-page"></a><a name="Introduction"></a> 簡介頁面

此頁面描述用於產生或發佈指令碼的步驟。

[不要再顯示此頁面]  - 下次啟動 [產生和發佈指令碼精靈]  時會略過此頁面。

  ![簡介頁面](media/generate-and-publish-scripts-wizard/intro.png)

### <a name="choose-objects-page"></a><a name="ChooseObjects"></a> 選擇物件頁面

您可以使用這個頁面來選擇哪些物件要包含在此精靈所產生的指令碼中。 在下列精靈頁面中，您可以選擇將這些指令碼儲存至所選擇的位置，或使用這些指令碼，將資料庫物件和資料發行至已安裝 [SQL Server 資料庫發行服務](https://go.microsoft.com/fwlink/?LinkId=142025) \(英文\) 的遠端 Web 主控提供者。

**編寫整個資料庫選項** - 選取即可針對資料庫中的所有物件產生指令碼，並且包含資料庫本身的指令碼。

   ![撰寫所有資料庫的指令碼](media/generate-and-publish-scripts-wizard/script-all.png)

**選取特定的資料庫物件** - 按一下即可限制此精靈只針對所選擇資料庫中的特定物件產生指令碼：

- **資料庫物件** ：至少選取一個要包含在指令碼中的物件。

- **全選** ：選取所有可用的核取方塊。

- **取消全選** ：清除所有的核取方塊。 您至少必須選取一個資料庫物件才能繼續。

   ![撰寫特定的指令碼](media/generate-and-publish-scripts-wizard/script-specific-objects.png)

### <a name="set-scripting-options-page"></a><a name="SetScriptOpt"></a> 設定指令碼編寫選項頁面

您可以使用這個頁面來指定要讓精靈將指令碼儲存至所選擇的位置，還是使用這些指令碼，將資料庫物件發行至遠端 Web 主控提供者。 若要發行，您必須取得使用資料庫發行服務 Web 服務所安裝之 Web 服務的存取權。

**選項** ：如果您想要讓精靈將指令碼儲存至所選擇的位置，請選取 **[將指令碼儲存至特定位置]** 。 您之後可以針對 Database Engine 執行個體或 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]執行指令碼。 如果您想要讓精靈將資料庫物件發行至遠端 Web 主控提供者，請選取 **[發佈到 Web 服務]** 。

**將指令碼儲存至特定位置**：將一或多個 Transact-SQL 指令碼檔案儲存至指定的位置。

![另存為筆記本](media/generate-and-publish-scripts-wizard/save.png)

- **[另存為筆記本](../../azure-data-studio/notebooks/notebooks-guidance.md)** - 將指令碼儲存至一個或多個 .sql 檔案。 選取瀏覽按鈕 ([...]  )，即可指定檔案的名稱和位置。

- **另存為指令檔** 將指令碼儲存至一個或多個 .sql 檔案。 選取瀏覽按鈕 ([...]  )，即可指定檔案的名稱和位置。 如果已經存在相同名稱的檔案，請選取 **[覆寫現有檔案]** 核取方塊來取代該檔案。 若要指定指令碼的產生方式，請選取 [單一指令檔]  或 [每一物件單一指令檔]  。 若要指定指令碼中應該使用的文字種類，請選取 [Unicode 文字]  或 [ANSI 文字]  。

- **儲存至剪貼簿** ：將 Transact-SQL 指令碼儲存至 [剪貼簿]。

- **在新增查詢視窗中開啟** - 在 Database Engine [查詢編輯器] 視窗中產生指令碼。 如果未開啟編輯器視窗，就會開啟新的編輯器視窗做為指令碼的目標。

- **進階** ：顯示可從中選取用於發佈指令碼之進階選項的 **[進階發佈選項]** 對話方塊。

- **提供者** ：選取提供者來指定 Web 主控服務的連接資訊，此服務會主控您想要在其中發佈所選取物件的資料庫。 **[管理提供者]** 對話方塊中至少必須有一個提供者，您才能選取提供者。

- **目標資料庫** ：選取您想要在其中發佈所選取物件的目標資料庫。 您必須先選取提供者，然後再選取目標資料庫。

### <a name="advanced-scripting-options-page"></a><a name="AdvScriptOpt"></a> 進階編寫指令碼選項頁面

您可以使用這個頁面來指定要如何讓此精靈產生指令碼。 這個頁面提供了許多不同的選項。 如果 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] [Database Engine 類型] **中指定的 SQL Server 或**版本不支援選項，選項會呈現灰色。

![進階選項](media/generate-and-publish-scripts-wizard/advanced.png)

**選項** - 在每個選項右方的可用設定清單中選取值，即可指定進階選項。

**一般**：下列選項適用於整個指令碼。

- **ANSI 填補** ：在指令碼中包含 **ANSI PADDING ON** 。 預設值為 **True**。

- **附加至檔案** ：設定為 **[True]** 時，這個指令碼會加入至 **[設定指令碼編寫選項]** 頁面上所指定的現有指令碼底部。 設定為 **[False]** 時，新的指令碼就會覆寫先前的指令碼。 預設值為 **False**。

- **檢查物件是否存在** - 當為 **True** 時，會先新增存在檢查，然後為 SQL 物件產生 CREATE 陳述式。 例如：資料表、檢視表、函式或預存程序。 CREATE 陳述式會包裝在 IF 陳述式中。 如果您知道目標是簡潔的，則指令碼就會簡潔得多。 如果您不希望這些物件存在於目標上，則會出現錯誤。 預設值為 **False**。

- **發生錯誤時繼續撰寫指令碼**：設定為 **False**時，指令碼撰寫會在發生錯誤時停止。 設定為 **True** 時，則會繼續撰寫指令碼。 預設值為 **False**。

- **將 UDDT 轉換為基底類型** ：設定為 **[True]** 時，使用者定義資料類型 (UDDT) 會轉換為用來建立它們的基礎基底資料類型。 當 UDDT 不存在於執行指令碼的資料庫時，請使用 [True]  。 設定為 **[False]** 時，就會使用 UDDT。 預設值為 **False**。

- **產生相依物件的指令碼** ：針對在執行所選取物件的指令碼時必須存在的物件產生指令碼。 預設值為 **True**。

- **包含描述性標頭** ：設定為 **[True]** 時，會將描述性註解加入至指令碼，並將指令碼分隔為代表每個物件的區段。 預設值為 **False**。

- **包含 if NOT EXISTS** ：設定為 **[True]** 時，此指令碼會包含檢查物件是否存在於資料庫的陳述式，而且如果該物件已經存在，就不會嘗試建立新物件。 預設值為 **False**。

- **包括系統條件約束名稱** ：設定為 [False]  時，會在目標資料庫上自動重新命名已在來源資料庫上自動命名之條件約束的預設值。 設定為 **[True]** 時，來源和目標資料庫的條件約束會具有相同的名稱。

- **包括不支援的陳述式** ：設定為 **[False]** 時，此指令碼不會包含所選取伺服器版本或引擎類型上不支援之物件的陳述式。 當設為 **[True]** 時，此指令碼包含不支援的物件。 對於不支援的物件而言，每個陳述式都會有陳述式必須編輯的註解，然後才可以針對選取的 SQL Server 版本或引擎類型來執行指令碼。 預設值為 **False**。

- **結構描述會限定物件名稱** - 在所建立物件的名稱中包含結構描述名稱。 預設值為 **True**。

- **指令碼繫結** ：產生用於繫結預設物件和規則物件的指令碼。 預設值為 **False**。 如需詳細資訊，請參閱 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md) 和 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)。

- [指令碼定序]  - 在指令碼中包含定序資訊。 預設值為 **False**。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。

- **編寫預設值的指令碼** ：包含用來在資料表資料行中設定預設值的預設物件。 預設值為 **True**。 如需詳細資訊，請參閱 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)。

- [編寫 DROP 和 CREATE 的指令碼]  - 設定為 [編寫 CREATE 指令碼]  時，會包含建立物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 設定為 **[編寫 DROP 指令碼]** 時，就會包含卸除物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 設定為 **[編寫 DROP 和 CREATE 的指令碼]** 時，就會針對每個編寫指令碼的物件，在指令碼中包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP 陳述式，後面接著 CREATE 陳述式。 預設值為 **編寫 CREATE 指令碼**。

- **編寫擴充屬性的指令碼** - 物件具有擴充屬性時，在指令碼中包含擴充屬性。 預設值為 **True**。

- **引擎類型的指令碼** - 建立可以在選取之類型的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 或 SQL Server Database Engine 執行個體上執行的指令碼。 指定的類型上所不支援的物件不會包含在指令碼中。 預設值為來源伺服器的類型。

- **針對伺服器版本編寫指令碼** ：建立可以在所選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本上執行的指令碼。 無法針對較舊的版本編寫某個版本新增功能的指令碼。 預設值為來源伺服器的版本。

- **編寫登入的指令碼** ：要為其編寫指令碼的物件是資料庫使用者時，這個選項會建立使用者相依的登入。 預設值為 **False**。

- **編寫物件層級權限的指令碼** ：包含於資料庫的物件上設定權限的指令碼。 預設值為 **False**。

- **編寫統計資料的指令碼** ：設定為 **[編寫統計資料的指令碼]** 時，此選項會包含 **CREATE STATISTICS** 陳述式以重新建立物件的統計資料。 **[編寫統計資料和長條圖的指令碼]** 選項也會建立長條圖資訊。 預設值為 **[不要編寫統計資料的指令碼]** 。 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)。

- [編寫 USE DATABASE 的指令碼]  - 在指令碼中加入 **USE DATABASE** 陳述式。 若要確定在正確的資料庫中建立資料庫物件，請包含 **USE DATABASE** 陳述式。 當指令碼要用於其他資料庫時，請選取 **False** 以省略 **USE DATABASE** 陳述式。 預設值為 **True**。 如需詳細資訊，請參閱 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)。

- **要撰寫指令碼的資料類型** - 選取應撰寫為指令碼的內容：[僅限資料]  ，[僅限結構描述]  ，或兩者。 預設值為 **[僅限結構描述]** 。

**資料表/檢視表選項** ：下列選項只適用於資料表或檢視表的指令碼。

- **編寫變更追蹤的指令碼** ：如果來源資料庫或來源資料庫中的資料表已啟用變更追蹤，則會編寫變更追蹤的指令碼。 預設值為 **False**。 如需詳細資訊，請參閱[關於變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)。

- **編寫 CHECK 條件約束的指令碼**：在指令碼中加入 **CHECK** 條件約束。 預設值為 **True**。 **CHECK** 條件約束會要求輸入資料表的資料必須符合某些指定的條件。 如需詳細資訊，請參閱 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)。

- [編寫資料壓縮選項的指令碼]  - 如果來源資料庫或來源資料庫中的資料表已設定資料壓縮選項，則會編寫資料壓縮選項的指令碼。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。 預設值為 **False**。

- **編寫外部索引鍵的指令碼** ：將外部索引鍵加入至指令碼。 預設值為 **True**。 外部索引鍵指出並強制執行資料表之間的關聯性。

- **編寫全文檢索索引的指令碼** - 編寫建立全文檢索索引的指令碼。 預設值為 **False**。

- **編寫索引的指令碼** ：編寫建立索引的指令碼。 預設值為 **True**。 索引可協助您快速尋找資料。

- **編寫主索引鍵的指令碼** ：編寫在資料表上建立主索引鍵的指令碼。 預設值為 **True**。 主索引鍵可唯一識別資料表的每個資料列。

- **編寫觸發程序的指令碼** - 編寫在資料表上建立 DML 觸發程序的指令碼。 預設值為 **False**。 DML 觸發程序是以程式設計當資料庫伺服器發生資料操作語言 (DML) 事件時所執行的動作。 如需詳細資訊，請參閱 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)。

- **編寫唯一索引鍵的指令碼** ：編寫在資料表上建立唯一索引鍵的指令碼。 唯一索引鍵可防止輸入重複的資料。 預設值為 **True**。 如需詳細資訊，請參閱 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)。

### <a name="summary-page"></a><a name="Summary"></a> 摘要頁面

![GS 摘要](media/generate-and-publish-scripts-wizard/summary.png)

這個頁面會摘要列出您在此精靈中所選取的選項。 若要變更選項，請選取 [上一步]  。 若要開始產生要儲存或發行的指令碼，請選取 [下一步]  。

**檢閱您的選取項目** ：針對精靈的每一個頁面，顯示您所選取的項目。 請展開節點以查看對應頁面的選取選項。

### <a name="save-or-publish-scripts-page"></a><a name="SavePubScripts"></a> 儲存或發佈指令碼頁面  

您可以使用這個頁面來監視此精靈執行的進度。

**詳細資料** ：若要查看此精靈的進度，請檢視 **[動作]** 欄。 產生指令碼之後，此精靈會根據您的選項，將指令碼儲存至檔案，或使用它們來發行至 Web 服務。 當每個步驟都完成之後，若要查看對應步驟的結果，請選取 [結果]  欄中的值。

**儲存報表** - 選取即可將精靈進度的結果儲存至檔案。

**取消** - 在處理完成之前或是發生錯誤時，選取即可關閉精靈。

**完成** - 在處理完成之後或是發生錯誤時，選取即可關閉精靈。

### <a name="save-scripts"></a>儲存指令碼

![[完成]](media/generate-and-publish-scripts-wizard/save-scripts-finish.png)

如果所有的設定都正確無誤，您的設定就會順利完成。

## <a name="generating-scripts-on-azure-synapse-analytics"></a>在 Azure Synapse Analytics 中產生指令碼

如果使用 "Script As..." 產生的語法，不像 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 語法，或者收到錯誤訊息，您可能需要將 SQL Server Management Studio 中的指令碼選項設為 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。

### <a name="how-to-set-default-scripting-options-to-sql-data-warehouse"></a>如何將預設指令碼選項設為 SQL 資料倉儲

若要使用 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 語法編寫物件的指令碼，請將預設的指令碼選項設為 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] ，如下所示︰

1. 依序選取 [工具]  與 [選項]  。
2. 在 [一般指令碼選項]  下方，設定下列項目：
    1. 資料庫引擎類型的指令碼：**Microsoft Azure SQL Database**。
    2. 資料庫引擎版本的指令碼：**Microsoft Azure SQL 資料倉儲版**。
3. 選取 [確定]  。

### <a name="how-to-generate-scripts-for-sql-data-warehouse-when-it-is-not-the-default-scripting-option"></a>如果適用於 SQL 資料倉儲的指令碼不是預設指令碼選項，該如何產生該指令碼

如果您將 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 設為預設指令碼選項 (如上所示)，即可忽略這些指示。 不過，如果您選擇使用不同的預設指令碼選項，則可能會遇到錯誤。 為了避免發生錯誤，請執行下列步驟以針對 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]產生和發佈指令碼：

1. 以滑鼠右鍵按一下您的 SQL 資料倉儲資料庫。
2. 選取 [產生指令碼]  。
3. 選擇您想要編寫指令碼的物件。
4. 在 [指令碼選項]  中，選取 [進階]  。 在 [一般]  下方，設定下列項目︰
    1. 資料庫引擎類型的指令碼：**Microsoft Azure SQL Database**。
    2. 資料庫引擎版本的指令碼：**Microsoft Azure SQL 資料倉儲版**。
5. 依序選取 [儲存或發佈指令碼]  與 [完成]  。

系統不會記憶步驟 4 所設定的選項。 如果您想要記憶這些選項，請遵循 **如何將預設指令碼選項設為 SQL 資料倉儲**中的指示。

## <a name="see-also"></a>另請參閱

- [安裝 SMO](../../relational-databases/server-management-objects-smo/installing-smo.md)

- [複製資料庫至其他伺服器](../../relational-databases/databases/copy-databases-to-other-servers.md)