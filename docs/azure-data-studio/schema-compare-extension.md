---
title: 結構描述比較延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure Data Studio 的結構描述比較延伸模組 (預覽)
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a51d64202d3d906b3106092084628b0a961297ea
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959320"
---
# <a name="schema-compare-extension-preview"></a>結構描述比較延伸模組(預覽)
結構描述比較延伸模組提供便於使用的體驗，比較 .dacpac 檔案和資料庫，並將來源的變更套用至目標。

此體驗目前為其初始預覽狀態。 請在[這裡](https://github.com/microsoft/azuredatastudio/issues)回報問題和功能要求。

## <a name="install-the-schema-compare-extension"></a>安裝結構描述比較延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視]  功能表中的 [延伸模組]  。
2. 選取可用的延伸模組，檢視詳細資料。
1. 選取您想要的延伸模組 (結構描述比較) 並加以**安裝**。

## <a name="how-do-i-start-a-schema-comparison"></a>如何開始進行結構描述比較？
* 結構描述比較的主要進入點是以滑鼠右鍵按一下物件總管中的資料庫，然後按一下 [結構描述比較]  。
* 使用者也可以從命令選擇區 (Ctrl+Shift+P) 搜尋 [結構描述比較]  ，啟動 [結構描述比較] 對話方塊

## <a name="why-would-i-use-the-schema-compare"></a>為什麼要使用結構描述比較？
結構描述比較的建立目的是為了新增比較 .dacpac 檔案和資料庫中的結構描述，以及套用變更的功能。

## <a name="next-steps"></a>後續步驟
若要深入了解結構描述比較，請[參閱我們的文件](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions)。


