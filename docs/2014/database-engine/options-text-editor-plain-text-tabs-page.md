---
title: 選項 （文字編輯器純文字的定位點頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
ms.assetid: 07d82d10-bca9-4b37-abbb-58ef9bfb264b
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5c27514ea38602885c26733238f2564211d4f43a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131779"
---
# <a name="options-text-editor---plain-text---tabs-page"></a>選項 (文字編輯器 - 純文字 - 定位點頁面)
  使用這個對話方塊可變更文字編輯器中按 Tab 鍵移動的行為，這個文字編輯器是用來編輯與特定開發語言沒有關聯的文件。 若要顯示這些設定，請按一下 [工具] 功能表上的 [選項]，展開 [文字編輯器]，展開 [純文字]，然後按一下 [定位點]。  
  
## <a name="setting-options-in-multiple-locations"></a>在多個位置設定選項  
 純文字編輯器的選項也可以在 **[所有語言 - 一般]** 對話方塊中設定。 如果您使用 **[所有語言]** 對話方塊為其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 編輯器 (例如 DMX 或 MDX 編輯器) 設定不同的選項，則必須使用這個對話方塊重設純文字編輯器。  
  
## <a name="indenting"></a>縮排  
 **無**  
 按下 ENTER 後，請勿縮排新建立的行。 資料指標會放在新行的第一個資料行上。  
  
 **區塊**  
 按下 ENTER 後，將新建立的行縮排至與前一行相同的縮排距離。  
  
 **智慧**  
 純文字編輯器不支援此格式類型。  
  
## <a name="tabs"></a>定位點  
 **定位點大小**  
 以空格數目，設定各定位點之間的距離。 預設值為四個空格。  
  
 **縮排大小**  
 以空格數目，設定自動縮排的大小。 預設值為四個空格。 將會插入定位字元、空格字元或兩者，以填滿指定的大小。  
  
 **插入空格**  
 縮排時僅插入空格字元而非定位字元。 例如，若 [縮排大小] 設定為 5，在您按下 TAB 鍵或在 [格式化] 工具列上按一下 [增加縮排] 按鈕時，就會插入五個空格字元。  
  
 **保留定位點**  
 縮排時儘可能插入最多的定位字元。 每個定位字元會填滿 **[定位點大小]** 中所指定的空格數目。 如果 [縮排大小] 不是 [定位點大小] 的偶數倍數，就會加入空格字元以填滿差異。  
  
  