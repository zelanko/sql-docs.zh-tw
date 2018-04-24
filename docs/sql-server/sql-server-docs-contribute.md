---
title: 如何參與編輯 SQL Server 文件集 | Microsoft Docs
ms.date: 04/12/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 380a7bebec1080f40ec10e3c59e6e1f105a5d2ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>如何參與編輯 SQL Server 文件集

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

大家都可以參與編輯 SQL Server 文件集。 這包括修正錯字、建議更好的說明，以及提升技術正確性。 本文說明如何開始參與編輯內容以及程序的運作方式。

若要參與編輯，您可以使用下列兩個主要的工作流程：

|||
|---|---|
| [在瀏覽器中編輯](#githubui) | 適合簡短、快速編輯任何文章。 |
| [使用工具以在本機編輯](#tools) | 適用於更複雜、涉及多篇文章的編輯，以及頻繁參與編輯 docs.microsoft.com。 |

## <a id="githubui"></a> 在瀏覽器中編輯

下列步驟提供在瀏覽器中對 SQL Server 內容進行簡單編輯的概觀。 完整程序記載於[適用於次要或不頻繁變更的 GitHub 參與工作流程](https://docs.microsoft.com/contribute/light-workflow)一文中。

1. 每篇文章 (包含本篇) 的右側都有一個 [編輯] 按鈕。 找到您想要變更的文章，然後按一下 [編輯] 按鈕即可開始。

   ![SQL 文件的 [編輯] 按鈕](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

   docs.microsoft.com 上的所有內容都是在各種 GitHub 存放庫中進行管理。 當您按一下 [編輯] 按鈕時，即會前往 **sql-docs** 存放庫中的文章。 或者，如果您要編輯 Azure 文件中的 SQL 文章，即會前往 **azure-docs** 存放庫。 

1. 接下來，按一下 GitHub 文章右上角的鉛筆圖示。

   ![[編輯] 按鈕](./media/sql-server-docs-contribute/edit-button.png)

   > [!NOTE]
   > 您必須登入 GitHub 才能編輯文章。 如果您沒有 GitHub 帳戶，請參閱 [GitHub 帳戶設定](https://docs.microsoft.com/contribute/get-started-setup-github)。 建立新帳戶後，您也必須向 GitHub 驗證電子郵件地址才可進行編輯。

1. 在瀏覽器中編輯文章。 所有文章都是以 Markdown 來撰寫。 如果您需要使用 Markdown 的說明，可以檢閱 [Markdown 基本概念](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)。 您也可以觀察並了解已發佈的文章如何呈現既有的 Markdown。

1. 向下捲動至 [編輯] 視窗底部，為您的變更輸入標題，然後按一下 [Propose file change] (提議檔案變更) 按鈕。

   ![建議提取要求](./media/sql-server-docs-contribute/propose-file-change.png)

1. 在下一個頁面上，按一下 [Create pull request] (建立提取要求)。

   ![建立提取要求](./media/sql-server-docs-contribute/create-pull-request.png)

1. 輸入提取要求的標題和描述。 然後再按一下 [Create pull request] (建立提取要求)。

   ![建立提取要求](./media/sql-server-docs-contribute/create-pull-request2.png)

此時，系統應該會引導您完成提取要求註解程序的其餘部分。 您可以在[參與者指南](https://docs.microsoft.com/contribute/light-workflow)中找到完整程序和其他詳細資料。

## <a id="tools"></a> 使用工具以在本機編輯

另一個編輯的選項是分叉 **sql-docs** 或 **azure-docs** 存放庫，並將其複製到本機電腦。 接著，您可以使用 Markdown 編輯器以及 git 用戶端將變更送出。 此工作流程適合進行較複雜或包含多個檔案的編輯。 它也很適合頻繁參與編輯 docs.microsoft.com 的使用者。

若要使用此方法參與編輯，請參閱下列文章：

- [建立 GitHub 帳戶](https://docs.microsoft.com/contribute/get-started-setup-github)
- [安裝內容撰寫工具](https://docs.microsoft.com/contribute/get-started-setup-tools)
- [本機設定 Git 存放庫](https://docs.microsoft.com/contribute/get-started-setup-local)
- [使用工具來參與編輯](https://docs.microsoft.com/contribute/full-workflow)

如果您送出對文件集的重大變更提取要求時，就會收到一個 GitHub 註解，要求您提交線上的**貢獻授權合約 (CLA)**。 您必須填妥線上表單，系統才會接受您的提取要求。

## <a name="recognition"></a>辨識

如果系統接受您的變更，文章上方就會辨識您為參與者。

![內容參與辨識](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>sql-docs 概觀

本節提供在 **sql-docs** 存放庫中進行作業的一些其他指引。

> [!IMPORTANT]
> 本節中的資訊是專用於 **sql-docs**。如果您要編輯 Azure 文件中的 SQL 文章，請參閱 [GitHub 中 azure-docs 存放庫的讀我檔案](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md)。

[sql-docs](https://github.com/MicrosoftDocs/sql-docs) 存放區會使用數個標準的資料夾來組織內容。

| 資料夾 | 描述 |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | 包含所有已發佈的 SQL Server 內容。 子資料夾會以邏輯方式組織內容的不同區域。 |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | 包含 include 檔案。 這些檔案是可能在一或多個其他主題中包含的內容區塊。 |
| **./media** | 每個資料夾都可以有一個 **media** 子資料夾，用來放置文章的影像。 **media** 資料夾中的子資料夾，其名稱與影像出現的主題名稱相同。 影像應該是 .png 檔案，檔名全為小寫字母且無空格。 |
| **TOC.MD** | 目錄檔案。 每個子資料夾都可以選擇使用一個 TOC.MD。 |

#### <a name="applies-to-includes"></a>applies-to include 檔案

每篇 SQL Server 文章標題後都包含一個 **applies-to** include 檔案。 這表示該文章適用哪些領域或 SQL Server 版本。

假設下列 Markdown 範例，其會在 **appliesto-ss-asdb-asdw-pdw-md.md** include 檔中提取。

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

這會將下列文字新增至文章的頂端：

![適用於文字](./media/sql-server-docs-contribute/applies-to.png)

若要為文章尋找正確的 applies-to include，請使用下列祕訣：

- 查看其他涵蓋相同功能或相關工作的文章。 如果您要編輯這篇文章，可以複製 Markdown 以取得 applies-to include 連結 (您可以取消編輯而不送出)。
- 搜尋 [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) 目錄，找出包含 "applies-to" 文字的檔案。 您可以使用 GitHub 中的 [尋找] 按鈕快速篩選。 按一下檔案以查看呈現的方式。
- 請注意命名慣例。 如果名稱中有 x，它們通常是預留位置，表示不支援服務。 比方說，**appliesto-xx-xxxx-asdw-xxx-md.md** 表示只支援 Azure SQL 資料倉儲，因為只拼寫出 **asdw**，而其他欄位均為 x。
- 某些 include 會指定版本號碼，例如 **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md**。 當您知道某項功能是由特定版本的 SQL Server 導入時，請只使用該版本的 include。 

## <a name="contributor-resources"></a>參與者資源

- [docs.microsoft.com 的參與者指南](https://docs.microsoft.com/en-us/contribute/)
- [Microsoft 樣式指南](https://docs.microsoft.com/en-us/teamblog/style-guide)
- [Markdown 基本概念](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> 如果您想提供產品的意見反應，而不是文件意見反應，請[在這裡提供 SQL Server 產品的意見反應](https://feedback.azure.com/forums/908035-sql-server)。

## <a name="next-steps"></a>後續步驟

探索 GitHub 上的 [sql-docs 存放庫](https://github.com/MicrosoftDocs/sql-docs)。

尋找文章、送出變更，並協助 SQL Server 社群。 

感謝您！


