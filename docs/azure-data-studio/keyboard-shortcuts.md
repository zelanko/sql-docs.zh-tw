---
title: 建立及自訂鍵盤快速鍵
titleSuffix: Azure Data Studio
description: 了解如何建立及自訂 Azure Data Studio 中的鍵盤快速鍵
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: b5a07ce70b57f5d62d53bf8ae9b570edcc78d7e6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800242"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>中的鍵盤快速鍵 [!INCLUDE[name-sos](../includes/name-sos.md)]

這篇文章提供快速檢視、 編輯和建立鍵盤快速鍵中的步驟[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

因為 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的按鍵繫結功能繼承自 Visual Studio Code，有關使用不同鍵盤配置等進階自訂內容的詳細資訊，請見 [Visual Studio Code 的按鍵繫結](https://code.visualstudio.com/docs/getstarted/keybindings) 文章。 某些索引鍵繫結功能可能無法使用 (比方說，快速鍵延伸模組不支援在[!INCLUDE[name-sos](../includes/name-sos-short.md)])。


## <a name="open-the-keyboard-shortcuts-editor"></a>開啟 鍵盤快速鍵編輯器

若要檢視所有目前定義的鍵盤快速鍵：

開啟**鍵盤快速鍵**從編輯器**檔案**功能表：**檔案** > **喜好設定** > **鍵盤快速鍵**( **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**  >  **偏好** > **鍵盤快速鍵**Mac 上)。

除了顯示目前的索引鍵繫結**鍵盤快速鍵**編輯器會列出可用的命令沒有定義的鍵盤快速鍵。 **鍵盤快速鍵**編輯器可讓您輕鬆地變更、 移除、 重設，並定義新的索引鍵繫結。  


## <a name="edit-existing-keyboard-shortcuts"></a>編輯現有的鍵盤快速鍵

若要變更現有的鍵盤快速鍵的按鍵繫結：

1. 找出您想要變更藉由使用 [搜尋] 方塊或清單中捲動的鍵盤快速鍵。
   > [!TIP]
   > 您可以依按鍵、 命令、 來源...等條件進行搜尋，以得到所有相關的鍵盤快速鍵搜尋結果。

1. 以滑鼠右鍵按一下所需的項目，然後選取**變更索引鍵繫結**

   ![編輯鍵盤快速鍵](media/keyboard-shortcuts/change-keybinding.png)

1. 按下所需的組合鍵，然後按下 **Enter** 儲存。 

   ![儲存鍵盤快速鍵](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>建立新的鍵盤快速鍵

若要建立新的鍵盤快速鍵：

1. 以滑鼠右鍵按一下 沒有任何索引鍵繫結，然後選取命令**新增金鑰繫結**。

   ![建立鍵盤快速鍵](media/keyboard-shortcuts/add-keybinding.png)

1. 按下所需的組合鍵，然後按下 **Enter** 儲存。


