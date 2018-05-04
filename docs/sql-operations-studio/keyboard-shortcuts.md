---
title: 建立及自訂鍵盤快速鍵，在 SQL Operations Studio （預覽） |Microsoft 文件
description: 了解如何建立及自訂 SQL Operations Studio （預覽） 中的鍵盤快速鍵。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8fc0bf7481401da9731106a578398a4b02bcd05
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>中的鍵盤快速鍵 [!INCLUDE[name-sos](../includes/name-sos.md)]

這篇文章提供快速檢視、 編輯和建立鍵盤快速鍵中的步驟[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

因為 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的按鍵繫結功能繼承自 Visual Studio Code，有關使用不同鍵盤配置等進階自訂內容的詳細資訊，請見 [Visual Studio Code 的按鍵繫結](https://code.visualstudio.com/docs/getstarted/keybindings) 文章。 某些按鍵功能可能無法使用 (例如，[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中不支援按鍵對應延伸模組)。


## <a name="open-the-keyboard-shortcuts-editor"></a>開啟 鍵盤快速鍵編輯器

若要檢視所有目前定義的鍵盤快速鍵：

從 **檔案** 功能表開啟 **鍵盤快速鍵** 編輯器：**檔案**  >  **喜好設定**  >  **鍵盤快速鍵** (Mac：**[!INCLUDE[name-sos](../includes/name-sos-short.md)]**  >  **喜好設定**  >  **鍵盤快速鍵**)。

除了顯示目前的按鍵組合**鍵盤快速鍵**編輯器列出可用命令沒有定義的鍵盤快速鍵。 **鍵盤快速鍵**編輯器可讓您輕鬆地變更、 移除、 重設，並定義新的按鍵組合。  


## <a name="edit-existing-keyboard-shortcuts"></a>編輯現有的鍵盤快速鍵

若要變更現有的鍵盤快速鍵的按鍵：

1. 找出您想要使用 [搜尋] 方塊，或捲動清單來變更的鍵盤快速鍵。
   > [!TIP]
   > 您可以依按鍵、 命令、 來源...等條件進行搜尋，以得到所有相關的鍵盤快速鍵搜尋結果。

1. 以滑鼠右鍵按一下所需的項目，然後選取**變更按鍵**

   ![編輯鍵盤快速鍵](media/keyboard-shortcuts/change-keybinding.png)

1. 按下所需的組合鍵，然後按下 **Enter** 儲存。  

   ![儲存鍵盤快速鍵](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>建立新的鍵盤快速鍵

若要建立新的鍵盤快速鍵：

1. 以滑鼠右鍵選取沒有按鍵綁定的命令，並選取**新增按鍵繫結**。

   ![建立鍵盤快速鍵](media/keyboard-shortcuts/add-keybinding.png)

1. 按下所需的組合鍵，然後按下 **Enter** 儲存。 


