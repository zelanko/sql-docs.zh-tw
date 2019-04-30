---
title: 針對 Azure Data Studio sandDance
titleSuffix: Azure Data Studio
description: 如何在 Azure 資料 Studio 中使用 SandDance
ms.custom: seodec18
ms.date: 04/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8fe968185f05c7a48415e5e158a20f4dc61b28c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63142190"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance 適用於 Azure 的資料 Studio （預覽）
Azure Data Studio 現在提供一種方式建立快速的視覺效果，您正在使用的.csv 和.tsv 檔案。 這在您的 SQL Server 2019 巨量資料叢集，包括本機檔案或在 HDFS 上的檔案。 當您嘗試將快速查看資料，並了解發生什麼情況，此延伸模組會有幫助。 我們會使用來自 Microsoft Research，可以產生資料的就地視覺效果稱為 SandDance 的技術。

![sanddance-animation](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

使用簡單易懂的檢視，SandDance 協助您尋找深入了解您的資料，它告訴劇本支援的資料，進而說明中建置根據辨識項的情況下，測試假設、 進一步了解到介面的說明、 支援決策購買，或讓資料放入更多的實際內容產生關聯。

SandDance 使用單位的視覺效果，其會套用在螢幕上的資料庫中的資料列和標記之間的一對一對應。
檢視之間的平滑動畫的轉換，可協助您維護內容，當您與您的資料互動。

## <a name="usage"></a>使用量

從 [檔案] 功能表中，使用開啟資料夾或 [Ctrl + K Ctrl + O] 來開啟包含的目錄。CSV 檔案。  接下來，從面板的 [總管] 中的.csv 或.tsv 檔案上按一下滑鼠右鍵並選擇*檢視中 SandDance*。

以滑鼠右鍵按一下在 HDFS 中的.csv 或.tsv 檔案如果您連線到 SQL Server 2019 巨量資料叢集，並選擇*檢視中 SandDance*。

## <a name="known-issues"></a>已知問題

目前您的資料應該具有第一個資料行，當做唯一識別碼。

目前我們不會限制以視覺化方式檢視的資料列計數。 不過，記憶體耗用量上去按比例的數字的資料列，因此我們建議的資料集或檢視，僅限於大約 100 萬個資料列。

請參閱[已知問題](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>版本資訊

### <a name="100"></a>1.0.0

Azdata sanddance 的初始版本

## <a name="next-steps"></a>後續步驟
若要進一步了解，[瀏覽 GitHub 存放庫。](https://github.com/Microsoft/SandDance)
