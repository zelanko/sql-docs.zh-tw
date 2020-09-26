---
title: 建立和自訂鍵盤快速鍵
description: 了解如何使用以 Visual Studio Code 中鍵盤快速鍵的功能，在 Azure Data Studio 中檢視、編輯和建立鍵盤快速鍵。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: fa4b5bc766b6d9bf269f08a1f00e2ef4d8c52b0e
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91363966"
---
# <a name="keyboard-shortcuts-in-azure-data-studio"></a>Azure Data Studio 的鍵盤快速鍵

本文提供在 Azure Data Studio 中快速檢視、編輯及建立鍵盤快速鍵的步驟。

由於 Azure Data Studio 會從 Visual Studio Code 繼承按鍵繫結關係功能，因此如需進階自訂、使用不同鍵盤配置等的詳細資訊，請參閱 [Visual Studio Code 的按鍵繫結](https://code.visualstudio.com/docs/getstarted/keybindings) (英文) 一文。 某些按鍵繫結功能可能不適用 (例如，Azure Data Studio 不支援按鍵對應延伸模組)。

## <a name="open-the-keyboard-shortcuts-editor"></a>開啟鍵盤快速鍵編輯器

若要檢視目前已定義的所有鍵盤快速鍵：

從 [檔案] 功能表開啟 [鍵盤快速鍵] 編輯器：[檔案] > [喜好設定] > [鍵盤快速鍵] (Mac 上為 [Azure Data Studio]  >  [喜好設定] > [快速鍵])。

除了顯示目前的按鍵繫結關係之外，[鍵盤快速鍵] 編輯器也會列出未定義鍵盤快速鍵的可用命令。 [鍵盤快速鍵] 編輯器可讓您輕鬆地變更、移除、重設和定義新的按鍵繫結關係。  

## <a name="edit-existing-keyboard-shortcuts"></a>編輯現有的鍵盤快速鍵

若要變更現有鍵盤快速鍵的按鍵繫結關係：

1. 使用搜尋方塊或捲動清單，尋找您要變更的鍵盤快速鍵。
   > [!TIP]
   > 依按鍵、命令、來源等搜尋，傳回所有相關的鍵盤快速鍵。

2. 以滑鼠右鍵按一下所需的項目，然後選取 [Change Key binding] \(變更按鍵繫結關係\)

   ![編輯鍵盤快速鍵](media/keyboard-shortcuts/change-keybinding.png)

3. 按下所需的按鍵組合，然後按 **Enter** 加以儲存。 

   ![儲存鍵盤快速鍵](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>建立新的鍵盤快速鍵

若要建立新的鍵盤快速鍵：

1. 以滑鼠右鍵按一下沒有任何按鍵繫結關係的命令，然後選取 [Add Key binding] \(新增按鍵繫結關係\)。

   ![建立鍵盤快速鍵](media/keyboard-shortcuts/add-keybinding.png)

2. 按下所需的按鍵組合，然後按 **Enter** 加以儲存。