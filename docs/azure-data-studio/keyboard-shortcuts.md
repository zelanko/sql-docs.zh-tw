---
title: 建立及自訂 Azure Data Studio 中的鍵盤快速鍵 |Microsoft Docs
description: 了解如何建立及自訂 Azure Data Studio 中的鍵盤快速鍵。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c6fb8d7e59441af00d3741ebc53756525d1cf3e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "48038011"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>中的鍵盤快速鍵 [!INCLUDE[name-sos](../includes/name-sos.md)]

這篇文章提供快速檢視、 編輯和建立鍵盤快速鍵中的步驟[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

因為 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的按鍵繫結功能繼承自 Visual Studio Code，有關使用不同鍵盤配置等進階自訂內容的詳細資訊，請見 [Visual Studio Code 的按鍵繫結](https://code.visualstudio.com/docs/getstarted/keybindings) 文章。 某些按鍵功能可能無法使用 (例如，[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中不支援按鍵對應延伸模組)。


## <a name="open-the-keyboard-shortcuts-editor"></a>開啟 鍵盤快速鍵編輯器

若要檢視所有目前定義的鍵盤快速鍵：

從 **檔案** 功能表開啟 **鍵盤快速鍵** 編輯器：**檔案**  >  **喜好設定**  >  **鍵盤快速鍵** (Mac：**[!INCLUDE[name-sos](../includes/name-sos-short.md)]**  >  **喜好設定**  >  **鍵盤快速鍵**)。

除了顯示目前按鍵繫結關係**鍵盤快速鍵**編輯器會列出可用的命令沒有定義的鍵盤快速鍵。 **鍵盤快速鍵**編輯器可讓您輕鬆地變更、 移除、 重設，並定義新按鍵繫結關係。  


## <a name="edit-existing-keyboard-shortcuts"></a>編輯現有的鍵盤快速鍵

若要變更現有的鍵盤快速鍵的按鍵繫結關係：

1. 找出您想要變更藉由使用 [搜尋] 方塊或清單中捲動的鍵盤快速鍵。
   > [!TIP]
   > 您可以依按鍵、 命令、 來源...等條件進行搜尋，以得到所有相關的鍵盤快速鍵搜尋結果。

1. 以滑鼠右鍵按一下所需的項目，然後選取**變更按鍵繫結關係**

   ![編輯鍵盤快速鍵](media/keyboard-shortcuts/change-keybinding.png)

1. 按下所需的組合鍵，然後按下 **Enter** 儲存。  

   ![儲存鍵盤快速鍵](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>建立新的鍵盤快速鍵

若要建立新的鍵盤快速鍵：

1. 以滑鼠右鍵選取沒有按鍵綁定的命令，並選取**新增按鍵繫結**。

   ![建立鍵盤快速鍵](media/keyboard-shortcuts/add-keybinding.png)

1. 按下所需的組合鍵，然後按下 **Enter** 儲存。 


