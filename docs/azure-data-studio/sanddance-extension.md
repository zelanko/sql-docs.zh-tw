---
title: 適用於 Azure Data Studio 的 SandDance
titleSuffix: Azure Data Studio
description: 如何在 Azure Data Studio 中使用 SandDance
ms.custom: seodec18
ms.date: 07/03/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a96bde6a66642bf02cc076c3d4d4f3ac44e02a3f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959336"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>適用於 Azure Data Studio 的 SandDance (預覽)
Azure Data Studio 現在可讓您為所使用的 .csv 和 .tsv 檔案建立快速視覺效果。 這包括 SQL Server 2019 巨量資料叢集中的本機檔案或 HDFS 檔案。 當您嘗試快速查看資料並了解發生的情況時，此延伸模組會很有幫助。 我們使用 Microsoft 研究的 SandDance 技術，可就地產生資料的視覺效果。

![SandDance 動畫](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

SandDance 利用容易了解的檢視，協助您深入解析資料，進而協助您陳述資料支援的劇本、以辨識項為依據建置案例、測試假設、深入表淺的說明進行探討、支援採購決策，或創造資料與更廣闊的真實世界內容之間的聯結。

SandDance 使用單元視覺效果，這會在您資料庫的資料列之間套用一對一對應，並在畫面上標示。
在檢視之間順暢地進行動畫轉換，可協助您在與資料互動時維持內容脈絡。

## <a name="usage"></a>使用方式

從 [檔案] 功能表開始，使用 [開啟資料夾] 或 [Ctrl+K Ctrl+O] 開啟包含 .CSV 的目錄。  接下來，從 Explorer 面板，以滑鼠右鍵按一下 .csv 或 .tsv 檔案，然後選擇 [在 SandDance 中檢視]  。

如果您已連線到 SQL Server 2019 巨量資料叢集，請以滑鼠右鍵按一下 HDFS 中的 .csv 或 .tsv 檔案，然後選擇 [在 SandDance 中檢視]  。

## <a name="known-issues"></a>已知問題

目前，您的資料應該以第一個資料行作為唯一識別碼。

我們目前並未限制視覺化的資料列計數。 不過，記憶體耗用量會隨著資料列數目按比例增加，因此建議您將資料集或檢視限制在約 10 萬個資料列。

請參閱[已知問題](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>版本資訊

### <a name="100"></a>1.0.0

azdata-sanddance 的初始版本

## <a name="next-steps"></a>Next Steps
若要深入了解，請[瀏覽 GitHub 存放庫](https://github.com/Microsoft/SandDance)。
