---
title: 結構描述比較延伸模組
description: 了解如何安裝和使用 Azure Data Studio 結構描述比較延伸模組，輕鬆比較兩個資料庫，並選擇性地變更其中一項以使其符合另外一項。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 35afe56806ad1c24b1fa6ae1f03978d7f6558af4
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123171"
---
# <a name="schema-compare-extension"></a>結構描述比較延伸模組

結構描述比較延伸模組提供容易使用的體驗，比較兩項資料庫定義，並將來源的差異性套用至目標。

## <a name="features"></a>特性

* 比較兩個 dacpac 檔案或資料庫的結構描述
* 以必須針對目標採取的動作集來檢視結果，以比對來源
* 選擇性排除結果中列出的動作
* 設定控制比較範圍的選項
* 將變更套用至目標，或產生具有相同效果的指令碼
* 儲存比較

![結構描述比較：範例比較](media/schema-compare-extension/schema-compare.png)

## <a name="why-would-i-use-the-schema-compare-extension"></a>為什麼要使用結構描述比較延伸模組？

手動管理和同步處理不同的資料庫版本可能相當繁瑣。 結構描述比較延伸模組可簡化資料庫比較程序，讓您在同步處理它們時可以全權控制 &mdash; 您可以選擇性地篩選特定的差異和差異類別，再套用變更。 結構描述比較延伸模組是可靠的工具，可節省您的時間並精簡程式碼。

![結構描述比較：[選項] 對話方塊](media/schema-compare-extension/schema-compare-options.png)

## <a name="install-the-extension"></a>安裝延伸模組

1. 選取延伸模組圖示以檢視可用的延伸模組。

    ![延伸模組管理員圖示](media/add-extensions/extension-manager-icon.png)

2. 搜尋並選取**結構描述比較**延伸模組，以檢視其詳細資料。 選取 [安裝] 以新增延伸模組。

3. 安裝之後，請**重新載入**以在 Azure Data Studio 中啟用延伸模組 (只有在第一次安裝延伸模組時才需要)。

## <a name="launch-a-schema-compare"></a>啟動結構描述比較

1. 若要開啟 [結構描述比較] 對話方塊，請以**滑鼠右鍵按一下** [物件總管] 中的資料庫，然後選取 [結構描述比較]。 您所選取資料庫會設定為比較中的來源資料庫。

    ![結構描述比較啟動功能表](media/schema-compare-extension/schema-compare-launch.png)

2. 選取其中一個省略號 (...) 來變更結構描述比較中的來源和目標，然後選取 [確定]。

    ![結構描述比較選取來源/目標](media/schema-compare-extension/schema-compare-select-source-target.png)

3. 若要自訂比較，請選取工具列中的 [選項] 按鈕。

4. 選取 [比較] 以檢視比較的結果。

## <a name="next-steps"></a>後續步驟

若要深入了解結構描述比較，請造訪[使用結構描述比較，比較不同的資料庫定義](../../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)。
請在[這裡](https://github.com/microsoft/azuredatastudio/issues)回報問題和功能要求。