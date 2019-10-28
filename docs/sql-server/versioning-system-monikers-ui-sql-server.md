---
title: 版本設定系統 SQL 文件 | Microsoft Docs
ms.date: 10/15/2019
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: conceptual
ms.reviewer: ''
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||>=sql-server-linux-2017||=sql-server-previousversions||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 7813368e08c8d1fdf4da1e2ee1e6775f56557d0a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907943"
---
# <a name="versioning-system-for-sql-documentation"></a>SQL 版本設定系統文件

[!INCLUDE[includes_appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文解釋我們的 SQL「版本設定系統」  文件。 版本設定系統了解產品及其版本。 系統可讓您選擇您有興趣的產品和版本。 系統接著會顯示適當的文件。

## <a name="applies-to-products"></a>適用對象產品

大多數的 SQL Server 文章都會在其標題下方包含**適用對象**文字。 在同一行上，接著會列出方便使用的 SQL「產品」  清單，指出文章是否與該產品相關。 例如，SQL Server 產品可能會標記為相關，但同時 Azure SQL Database 則可能會標記為與文章無關。

**適用對象**一行不了解產品的「版本」  。 我們會努力避免**適用對象**一行和我們版本設定系統設定產品面之間的不一致。

## <a name="history-of-separate-file-sets"></a>個別檔案集歷程記錄

針對 SQL Server 2014 及更早的版本，每個版本都有自己個別的完整文件檔案複本。 例如，SQL Server 2014 文件會從 SQL Server 2012 的文件複本開始。 2014 的複本接著會在產品開發週期期間進行編輯。

這種舊方法表示若在 2014 的文件中發現問題，2012 和 2008 的文件中也可能會存在該問題。 這會讓修正問題和一般維護變得更為困難。

## <a name="multiple-versions-in-the-same-files"></a>相同檔案中的多個版本

基於此原因和其他因素，SQL Server 2016 的文件檔案也適用於 2017、2019，且可能適用於 \<vNext\>。 這項合併相當實用，因為我們現在會將「版本設定 moniker」  指派給我們的 SQL Server 文件檔案。 版本設定 moniker 會根據每個指定文件檔案合理的細微性程度進行指派或明確內嵌。

## <a name="versioning-control-in-the-ui"></a>UI 中的版本設定控制

當您使用我們的 :::no-loc text="Docs"::: 網站檢視任何 SQL 文件文章時，您可以在目錄 (TOC) 的上方看見目前選擇的版本設定 moniker。 該控制項是一個下拉式清單。

![media_versioning-control-10-sql-server-2017.png](media/versioning-control-10-sql-server-2017.png)

若您想要查看不同 SQL Server 版本的文件，您可以按一下位於目前版本 moniker 結尾的擴張箭號。 然後按一下來選擇您想要的任何產品及版本組合。 當您按一下不同版本時，所顯示的文件會立即變更，以顯示新選擇版本的差異。 可能會有變更，也可能不會有任何變更；這兩種案例都很常見。

![media_versioning-control-20-expanded.png](media/versioning-control-20-expanded.png)

### <a name="https-parameter-no-loc-textview"></a>HTTPS 參數 :::no-loc text="view=":::

每個網址開頭是 `https://docs.microsoft.com/sql/` 之文章都會在其網址上附加名為 `?view=` 的參數。 此參數值是版本控制 moniker 程式碼。

`https` 網址中的 moniker「程式碼」  一律會和版本設定控制項中顯示的 moniker「名稱」  相符。

## <a name="products-not-editions"></a>產品，並非版本

### <a name="editions"></a>版本

在 1990 到 2000 年代間，Microsoft SQL Server 只有一個產品。 每個 SQL Server 版本都有各種「版本」  ，例如 SQL Server 2008 的 _Developer_ 和 _Enterprise_ 版本。 版本會包含稍微不同的功能集，但核心產品都是相同的。 新的 SQL Server 版本仍然可能會有各種版本。

### <a name="products"></a>產品

隨著近年雲端運算和 Microsoft Azure 的崛起，Microsoft 發行了 Azure SQL Database 產品。 雖然傳統式 SQL Server 內部部署產品和 Azure SQL Database 產品共用了許多程式碼，但這兩個產品是真正各自獨立的產品。

針對 SQL，版本設定 moniker 會區別產品間的差異，但不會區別版本間的差異。

#### <a name="azure-cloud-sql-products"></a>Azure 雲端 SQL 產品

針對整個網址開頭為 `https://docs.microsoft.com/sql/` 的文章，幾乎全部都適用於至少一個名為 SQL Server 產品的版本。 這些文章的大部分也適用於一或多個我們裝載在 Azure 雲端上 SQL 服務產品。 其中的一項 SQL 雲端產品名為 Azure SQL Database。

自然地，Azure SQL Database 產品只有一個版本。 幾乎所有適用於 Azure SQL Database 但不適用於 SQL Server 的文章，其網址開頭都是 `https://docs.microsoft.com/azure/sql-database/`。

## <a name="scenarios-of-version-filtering"></a>版本篩選案例

版本設定系統運作方式是篩選掉所有不適用於目前使用中 moniker 的文件內容。 每次您選擇不同的版本設定 moniker 時，隱藏的內容集便會變更。 篩選會在下列層級隱藏內容：

- 文章內的區段或句子。
- 目錄 (TOC) 中的文章項目。

以下是解釋選擇不同 moniker 效果的案例。

### <a name="scenario-1-within-the-current-article"></a>案例 1：在目前文章內

下列案例會聚焦於您目前文章內的區段：

1. 目前的版本設定 moniker 是 **SQL Server 2017**。
2. 您正在閱讀一個區段，描述最早於 SQL Server 版本 2017 新增的功能。
3. 您將 moniker 變更為 **SQL Server 2016**。
4. 您會察覺您正在閱讀的區段已消失。
5. 您再次變更 moniker，但這一次是變更為 **SQL Server 2019**。
6. 您會察覺您正在閱讀的 2017 區段已重新顯示。

在上述案例中，新的 2017 功能區段可能會以「moniker 範圍」  進行標記，其中可能包含下列 moniker 程式碼：

- `>=sql-server-2017`

選擇 moniker **SQL Server 2019** 時，版本設定系統便會了解 2019 大於或等於 2017，並顯示該區段。

### <a name="scenario-2-click-a-link-to-a-hidden-article"></a>案例 2：按一下連結來隱藏文章

下列不常見案例會解釋當您按一下某一篇文章的連結，但目錄 (TOC) 目前正隱藏該文章時，會發生什麼情況。 簡單來說，連結的運作方式為：

1. 目前的版本設定 moniker 是 **SQL Server 2017**。
2. 在目前的文章 :::no-loc text="A"::: 中，您按一下僅適用於 SQL Server 2016 的文章 :::no-loc text="B"::: 連結。
    - 在按一下之前，目錄會隱藏文章 :::no-loc text="B"::: 的項目。
3. 在按一下之後，會隨即顯示文章 :::no-loc text="B":::。
    - 顯示文章 :::no-loc text="B"::: 會強制版本設定控制項切換至 **SQL Server 2016** moniker。
    - 因為必須放棄原始的 moniker **SQL Server 2017**。 這段放棄的過程會在網頁接近頂端的位置顯示一個資訊訊息。 該[訊息](#anchor-message-unavailable-for-moniker)會解釋目前的 moniker 必須進行切換，以適應新的文章 :::no-loc text="B":::。

### <a name="scenario-3-navigate-to-an-https-address"></a>案例 3：巡覽至 HTTPS 位址

下列文章是針對 SQL Server 2017 新增的。 文章會描述在版本 2017 中新增至 SQL Server 的功能。 大多數或所有這些新功能也都是版本 2019 的一部分。 以下是文章的屬性。

| attribute | ReplTest1 |
| :-------- | :---- |
| Title | SQL Server 2017 的新功能 |
| moniker 範圍 | `>= sql-server-2017 || = sqlallproducts-allversions` |
| `https` 位址 | `https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017` |
| &nbsp; | &nbsp; |

有鑑於基底 `https` 位址，下表會解釋在使用者附加 `?view=` 參數及各種值時會發生什麼情況。

| `?view=` 的值 | `https` 位址導覽的行為 |
| :---------------- | :------------------------------ |
| (無參數。)  | 版本設定系統會嘗試其預設的 moniker 值。 通常我們會將此設為最新的 SQL Server 非預覽版本。<br/><br/>SQL Server 2017 或 2019 的預設會滿足屬性 `>= sql-server-2017`。<br/><br/>系統會將參數附加到 `https` 位址 (也許是 `?view=sql-server-2017`)。<br/>版本設定下拉式清單控制項接著會設為相符的 moniker 名稱。 |
| `sql-server-2016` | 版本設定系統會了解到文章的 moniker 範圍不包含版本 2016。<br/><br/>系統接著會選擇其中一個滿足範圍的 moniker。<br/><br/>然後正如同版本 2016 的案例，會附加 `?view=` 參數，且控制項名稱會和參數值相符。 |
| `sql-server-2017` | 版本設定系統了解參數值包含在文章的 moniker 範圍內。<br/><br/>版本設定控制項會設為與參數值相符。 |
| `sql-server-2019` | 這也適用於值為 `sql-server-2017` 的案例，差別僅在參數和控制項會設為 2019。 |
| &nbsp; | &nbsp; |

### <a name="anchor-allsql-hidenothing"></a> 所有 SQL - 不隱藏項目，特殊的 moniker

有一個特殊的 moniker 產品名稱是**所有 SQL**，且其唯一的版本是**不隱藏項目**。 此 moniker 的目的是用於在內部測試特定變更。 若由客戶使用，則相較於通知，此 moniker 更可能會誤導客戶。

有些文章包含與多個 SQL Server 版本相關的資訊。 每個一般 moniker 都會隱藏已建立版本的區段；這些區段原先可能會顯示 moniker 版本的不正確、令人困惑或矛盾資訊。 特殊的**所有 SQL** moniker 會顯示所有版本區段，且顯示不正確的資訊時可能並不明顯。

## <a name="anchor-message-unavailable-for-moniker"></a> 訊息：要求的頁面無法提供 \<moniker\> 使用

下列案例會導致在 :::no-loc text="Docs"::: 網頁接近頂端的位置顯示資訊訊息：

1. 目前的版本設定 moniker 為 **SQL Server 2017**。
2. 您正在閱讀與 SQL Server 2017 相關的文章。
    - 文章與 Azure SQL Database 產品「無關」  。
3. 您嘗試將 moniker 變更為 **Azure SQL Database - 目前**。
4. 您會看到您的嘗試遭到拒絕，且顯示一個訊息。

在此案例的最後，您會看到資訊訊息顯示在 Docs 網頁接近頂端的位置：

> 所要求的頁面無法提供 Azure SQL Database - 目前使用。 您已重新導向到此頁面適用的最新產品版本。

「最新」  版本可能會排除尚未完全發行，且處於「預覽」  狀態的版本。

![media_versioning-control-30-viewfallbackfrom.png](media/versioning-control-30-viewfallbackfrom.png)

## <a name="previous-versions-of-sql-server"></a>先前的 SQL Server 版本

版本設定系統已為 SQL Server 2016 版本之後的版本完全實作。

- 2012 及較舊版本：  &nbsp; SQL Server 2012 及較舊的版本並未使用版本設定系統。
    - **SQL Server - 舊版**的特殊 moniker 旨在隱藏幾乎所有文章。 少見的例外狀況是舊版客戶可能一次只需要幾篇文章。
    - [SQL Server 的先前版本，2012-2005](../toc/previous-versions-sql-server.md)

- 2014：  &nbsp; 版本設定系統已為 SQL Server 2014 實作一半。 您可以在版本設定控制項中選擇 SQL Server 2014，它會正常運作。 但是在內部，2014 的檔案仍僅專屬於 2014，也就是和 2008 的檔案僅專屬於 2008 相同。
    - [SQL Server 2014 文件](/sql/2014-toc/books-online-for-sql-server-2014?view=sql-server-2014)

- 2016 及更新版本：  &nbsp; 版本設定系統已為 SQL Server 2016 及更新版本完全實作。
    - [歡迎使用 SQL Server 文件 2016 及更新版本](/sql/sql-server/index.yml?view=sql-server-2016)

## <a name="see-also"></a>另請參閱

[SQL Server 的先前版本，2014-2005](../toc/previous-versions-sql-server.md)  
[SQL Server 文件導覽指南](sql-docs-navigation-guide.md)  
[如何參與 SQL Server 文件](sql-server-docs-contribute.md)  
