---
title: 什麼是 SSMA for Access(AccessToSQL) 新功能 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 02/27/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 40d5daaaef68d4355a95fb6cef2c55628cdf4008
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955919"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA for Access (AccessToSQL) 中最新消息
本文章列出 SQL Server Migration Assistant (SSMA) 的每個版本中的存取權變更。  

## <a name="ssma-v80"></a>SSMA v8.0
SSMA for Access 8.0 版發行已經過增強，以提供目標式的修正，旨在改善品質和轉換的計量。 此版本也提供了下列新功能：

* 支援**Azure SQL Database 受控執行個體**做為目標。 您現在可以建立新的專案目標 Azure SQL Database 受控執行個體：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

*   轉換後**修正 advisor**。 深入了解[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)。

* 初步的資料庫/結構描述選取範圍。

    連接到來源時，使用者現在可以選取感興趣的資料庫/結構描述。 選取您要移轉的結構描述，會將儲存初始連線期間的時間，並改善整體的 SSMA 效能。

    ![SSMA 篩選物件](../media/ssma-filter-objects.png)

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。


## <a name="ssma-v710"></a>SSMA v7.10
SSMA for Access v7.10 發行的增強提供目標式修正，旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for Access v7.9 版本包含下列變更：
- 目標式的修正，可改善品質和轉換的計量。
- 支援變更資料類型對應和專案的喜好設定的 SSMA 命令列中。
- SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變指定完整的伺服器名稱。 在舊版的 SSMA，Azure SQL Database 的前置詞必須明確提及在專案設定。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v78"></a>SSMA v7.8
SSMA for Access v7.8 版本包含下列變更：
- 專案設定中的反白顯示的變更型別對應。
- 提供可讓使用者以停用遙測。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Access v7.7 版本包含下列變更：
- SSMA for Access 已經過加強，以改善品質和轉換計量的目標式修正。
- 32 位元版本的 SSMA for Access 依據熱門的需求，已經恢復。 相較於先前的實作 （在之前 v7.4)，有兩個安裝程式套件，但它們無法並存安裝。 如此一來，您必須選擇您所擁有的最適當版本的連線元件為基礎。 一律最好是使用 64 位元版本，如果可能的話。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Access v7.6 版本已經過加強，改善品質和轉換計量的目標式修正與 SQL Server 2017 （公開預覽） 的支援。 在 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，並不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件，與 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for Access v7.5 版本已經過加強，以確保更高的協助工具，方便殘障人士使用的數個改進功能。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Access v7.4 版本包含下列變更：
- **查詢逾時**選項已經可以使用在來源和目標結構描述物件探索期間。
![查詢逾時選項](../media/query-timeout_red.png)

- 品質和轉換的計量，而改善了目標式修正，根據客戶意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Access v7.3 版本包含下列變更：
- 改善的品質和轉換度量目標式修正，根據客戶意見反應。
- SSMA 擴充性架構，透過下列項目公開：
  - 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    -   您現在可以從 SSMA 匯出結構描述指令碼，SSDT 專案。 您可以使用結構描述指令碼來進行其他的結構描述變更及部署您的資料庫。
![將儲存為 SSDT 專案命令](../media/export-schema-scripts_red.png)

  - 可供執行自訂轉換的 SSMA 的程式庫。
    - 您現在可以建構自訂的語法轉換和轉換先前未處理的 SSMA 可以處理的程式碼。
      - 在此部落格文章中，可指示如何建構自訂轉換器[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 下載範例專案進行轉換，從此[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2
SSMA for Access v7.2 版本包含下列變更：
- 改善的品質和轉換度量目標式修正，根據客戶意見反應。
- 若要提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換率的遙測增強功能。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access v7.1 版本包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 現支援的目標平台進行移轉。 這項功能處於技術預覽狀態，並支援結構描述和資料移動至目標 SQL server。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，因為它位於。
- SSMA 安裝二進位檔現在都是透過 Windows installer 套件檔案 (.msi) 提供。

**資源**

[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>2016 年  
SSMA for Access 2016 5 月版本包含下列變更：  
  
-  已新增的官方支援，適用於 SQL Server 2016
-  已移除適用於.Net 2.0 的安裝程式檢查。
-  已修正 儲存專案 」 和 SSMA 主控台的 開啟專案 命令。
-  SSMA 主控台中修正 「 securepassword"命令。
-  已修正的初始載入的物件計數。
-  已修正資料表的資料載入 UI 索引標籤存取。
-  全域設定中已修正的 bug。 
   
## <a name="march-2016"></a>2016 年 3 月  
SSMA for Access 的 2016 年 3 月預覽版本包含下列變更：  
  
-  新增的移轉至 SQL Server 2016 的支援。  
   
## <a name="january-2016"></a>2016 年 1 月  
SSMA for Access 的 2016 年 1 月維護版本包含下列變更：  
  
-  固定函式無效的預設值是 GUID 欄位 (RFC 3894811)。  
-  已修正匯入到 SQL Database (Azure) (RFC 4919573) 的記錄的停止回應。  
-  新增的檢視至 SSMA (RFC 5706203) 的記錄功能表項目。  
-  已新增的遙測。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Access 的 2014 年 7 月版本包含下列變更：  
  
-   改善的 Azure SQL DB 的程式碼轉換。  
-   移到 結構描述，以支援 Azure SQL DB 的延伸模組組件功能。  
-   針對具有超過 10 萬個物件的資料庫已測試的效能改善。  
-   已新增的 UI 增強功能來處理大量的物件。  
-   已新增的支援的反白顯示 「 已知 」 的 LOB 結構描述 （因此它們可以在轉換中應忽略）。  
-   新增轉換速度改善。
-   已新增的支援，來顯示物件計數的 UI 中。
-   減少的報表的大小超過 25%。
-   未剖析的建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Access 的 2014 年 4 月版本包含下列變更：  
  
-   已新增的支援 MS SQL Server 2014。  
-   關於轉換至 Azure 已經修正的 bug。  
-   已修正的 IE 10 中的不可見的報表頁面相關的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Access 的 2012 年 1 月版本包含下列變更：  
  
-   提供的選項不會保存使用者名稱和密碼的 MS Access 移轉之後連結的資料表。  
-   設定為 No Action 的循環參考的重疊顯示動作。  
-   提供適當的訊息，指出循環參考的重疊顯示動作，已設定為 No Action。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Access 的 2011 年 7 月版本包含下列變更：  
  
-   資料移轉期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Access 的 2011 年 4 月版本包含下列變更：  
  
-   新增可安裝的 「 SSMA for Access 」，可支援單一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"] 和 [Azure SQL。  
-   新增連線能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
-   已新增的 SSMA for Access 主控台版本支援回溯相容性。 您可以開啟 SSMA v5.0 稍早的版本所建立的專案。
-   新增與較舊版本的 SSMA 產品安裝 SSMA v5.0 產品並存 (SxS) 的能力。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Access 2010 年 7 月版本包含下列變更：  
  
-   已新增的支援移轉至 SQL Server 2008 R2 和 Azure SQL。
-   加入 SQL Server 和 Azure SQL 的安全連線。  
-   已新增的支援 Access 2010 資料庫。
-   加入新的 SSMA 主控台應用程式的命令列執行。
-   已新增的支援 SQL Server DateTime2 資料類型。
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Access 的 2008 年 6 月版本包含下列變更：  
  
-   Access 2007 資料庫所新增的支援。  
  
## <a name="may-2007"></a>2007 年 5 月  
SSMA for Access 2007 年版本包含下列變更：  
  
-   已新增的支援使用群組原則的 Access 資料庫。  
-   提供能夠從 SQL Server 中繼資料總管 中刪除已轉換的物件。  
-   已新增的支援 SQL Server 中的使用者輸入註解格式 SQL 模式。  
-   已新增的進步物件轉換的詳細資訊。  
  
## <a name="november-2006"></a>2006 年 11 月  
SSMA for Access 的 2006 年 11 月版本包含下列變更：  
  
-   加入新的資料庫移轉精靈可引導您完成移轉單一資料庫的存取權從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
-   加入新的轉換，負載，並將 Access 資料庫的 [移轉] 命令載入轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]全都放在一個步驟。  
-   改善的查詢的移轉。 現在將選取要檢視的查詢，請查詢移轉。 如需詳細資訊，請參閱 [ 轉換的 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。  
-   加入編輯資料表和索引的屬性上的功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**資料表** 索引標籤。  
-   新增新的全域設定：  
    -   您可以選擇在編輯器視窗中顯示行號。  
    -   您可以設定 SSMA 提示來取代重複的物件，或一律或永遠不會取代重複的物件結構描述轉換期間。  
-   加入新的轉換選項，可讓您指定在複雜的查詢包含萬用字元時，SSMA 是否顯示警告。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月版本的 SSMA for Access 是初始版本。
