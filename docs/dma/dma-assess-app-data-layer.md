---
title: 使用 Data Migration Assistant 評估應用程式的資料存取層
description: 瞭解如何使用 Data Migration Assistant 來評估應用程式的資料存取層。
ms.date: 01/23/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 13b0775dd7a20d37e80eaddb39f649f65c43b129
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886175"
---
# <a name="assess-an-apps-data-access-layer-with-data-migration-assistant"></a>使用 Data Migration Assistant 評估應用程式的資料存取層

應用程式通常會將資料連線並保存到資料庫。 應用程式的資料存取層可簡化此資料的存取。 Data Migration Assistant （DMA）已啟用使用者評估其資料庫和相關物件。 最新版本的 DMA （v 5.0）引進了在應用程式代碼中分析資料庫連接和內嵌 SQL 查詢的支援。

請考慮下列 c # 程式碼片段：

![範例 c # 程式碼區段](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-segment.png)

在此情況下，您可以看到應用程式使用 SQL 查詢來取得員工的名稱。

![範例 c # 程式碼區段詳細資料](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-detail.png)

身為應用程式擁有者，我必須能夠識別應用程式可以連接的各種資料庫，以及內嵌在應用程式資料存取層中的查詢。 此外，我還需要識別將應用程式現代化到 Azure 資料服務所需的任何變更。

## <a name="assess-an-app-with-data-access-migration-toolkit"></a>使用資料存取遷移工具組評估應用程式

為了實現這種評量，我們最近引進了資料存取遷移工具組（DAMT），這是一個 Visual Studio Code 的延伸模組。 此延伸模組的最新版本（v 0.2）新增對 .Net 應用程式和 T-sql 方言的支援。

1. 從[這裡](https://code.visualstudio.com/download)下載並安裝 VS Code。
2. 從擴充功能 Marketplace 啟用[資料存取遷移工具組延伸](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)模組。

   ![資料存取遷移工具組延伸模組頁面](../dma/media/dma-assess-app-data-layer/dma-damt-extension-page.png)

3. 在 Visual Studio Code 中開啟應用程式專案。

   ![Visual Studio Code 中的應用程式專案](../dma/media/dma-assess-app-data-layer/dma-app-project-in-vscode.png)

4. 啟動延伸模組主控台（Ctrl-Shft-P），然後執行 [**資料存取：分析工作區**] 命令。

   ![Visual Studio Code 中的延伸模組主控台](../dma/media/dma-assess-app-data-layer/dma-vscode-extension-console.png)

5. 選取 SQL Server 方言。

   ![SQL Server 用語選擇](../dma/media/dma-assess-app-data-layer/dma-sql-server-dialect.png)

   在分析結束時，此命令會產生 SQL 連線命令和查詢的報告。

   ![資料存取報表](../dma/media/dma-assess-app-data-layer/dma-data-access-report.png)

6. 檢查資料連線元件的報表，以及內嵌在應用程式代碼中的 SQL 查詢（反白顯示）。

   ![應用程式程式碼中的 SQL 查詢](../dma/media/dma-assess-app-data-layer/dma-sql-queries-in-app-code.png)

   這些查詢可以透過 DMA 分析，以瞭解以目標 SQL 平臺為基礎的相容性和功能同位問題。

7. 若要評估應用程式的資料層，請將報表匯出為 json 檔案。

   ![. json 檔案匯出](../dma/media/dma-assess-app-data-layer/dma-json-file-export.png)

   在此情況下，產生的檔案為：

   ![查看 json 檔案的內容](../dma/media/dma-assess-app-data-layer/dma-json-file-contents.png)

   Data Migration Assistant 可讓您在將資料庫現代化至 Azure 資料平臺的內容中，評估應用程式中識別的查詢。

8. 啟動 Data Migration Assistant，然後建立評量專案。

   ![Data Migration Assistant 新的評估專案](../dma/media/dma-assess-app-data-layer/dma-new-assessment-project.png)

9. 選取來源 SQL Server 實例。

   ![Data Migration Assistant 選取 SQL Server 來源](../dma/media/dma-assess-app-data-layer/dma-select-sql-source.png)

10. 選取應用程式所連接的資料庫。

    ![資料存取遷移選取應用程式資料庫](../dma/media/dma-assess-app-data-layer/dma-select-app-database.png)

    為了加速資料存取評估，DMA 引進了在應用程式查詢中包含 json 檔案的功能。 接下來，我們會包含我們稍早在應用程式查詢中所製作的 json 檔案。

11. 選取資料庫，並流覽至從資料存取遷移工具組匯出的 json 檔案，以包含應用程式中的查詢進行評估。

    ![Data Migration Assistant 開啟 DMAT json 檔案](../dma/media/dma-assess-app-data-layer/dma-open-damt-json-file.png)

12. 開始評量。

    ![Data Migration Assistant 開始評估](../dma/media/dma-assess-app-data-layer/dma-start-assessment.png)

13. 審查評量報告。 產生的報告將會包含在應用程式查詢中偵測到的任何相容性或功能同位問題，如下所示。

    ![Data Migration Assistant 評量報告](../dma/media/dma-assess-app-data-layer/dma-assessment-report.png)

現在，除了讓資料庫瞭解遷移的觀點之外，使用者也會從應用程式的觀點來看。

## <a name="see-also"></a>另請參閱

* [Data Migration Assistant 總覽](../dma/dma-overview.md)
* [Data Migration Assistant：設定](../dma/dma-configurationsettings.md)
* [Data Migration Assistant：最佳做法](../dma/dma-bestpractices.md)
* [資料存取移轉工具組](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)