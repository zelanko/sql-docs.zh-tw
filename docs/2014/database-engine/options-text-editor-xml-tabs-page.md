---
title: 選項（文字編輯器： XML：定位點頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Tabs
ms.assetid: 13bf5f8c-aba3-4c05-b8bb-eb475797c9bd
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: ae595b42274e012032e79754650b573b5d80053b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089124"
---
# <a name="options-text-editorxmltabs-page"></a>選項 (文字編輯器：XML：定位點頁面)
  這個對話方塊可以讓您變更在 XML 編輯器中按下 Tab 鍵的移動行為，這個編輯器會用來編輯 XML 文件。 若要顯示這些設定，請按一下 **[工具]** 功能表上的 **[選項]** ，展開 **[文字編輯器]** 資料夾，展開 **[XML]** 子資料夾，然後按一下 **[定位點]**。  
  
## <a name="setting-options-in-multiple-locations"></a>在多個位置設定選項  
 XML 編輯器的選項也可以在 **[所有語言 - 一般]** 對話方塊中設定。 如果您使用 **[所有語言]** 對話方塊為其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 編輯器 (例如 DMX 或 MDX 編輯器) 設定不同的選項，則必須使用這個對話方塊重設 XML 編輯器選項。  
  
## <a name="indenting"></a>縮排  
 **None**  
 如果選取此選項，當您按下 ENTER 時所建立的新行就不會縮排。 資料指標會放在新行的第一個資料行上。  
  
 **總匯**  
 如果選取此選項，當您按下 ENTER 鍵時所建立的新行就會自動縮排與上一行相同的距離。  
  
 **智慧型**  
 如果選取此選項，當您按下 ENTER 時所建立之新行的位置，就會根據內容而定。 例如，在左大括號 ({) 之後，其中的行會自動增加一個定位點的縮排距離。 對應的右大括號 (}) 則與左大括號重新對齊。  
  
## <a name="tabs"></a>定位點  
 **定位點大小**  
 以空格數目，設定各定位點之間的距離。 預設值為四個空格。  
  
 **縮排大小**  
 以空格數目，設定自動縮排的大小。 預設值為四個空格。 會插入定位字元、空格字元或兩者，以填滿指定的大小。  
  
 **插入空格**  
 如果選取此選項，縮排作業僅會插入空格字元，而非定位字元。 例如，如果 [**縮排大小**] 設為5，則每當您按下 TAB 鍵或在主[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]視窗的工具列上按一下 [**增加縮排**] 按鈕時，就會插入五個空白字元。  
  
 **保留定位點**  
 如果選取此選項，縮排作業會儘可能插入最多的定位字元。 每個定位字元會填滿 **[定位點大小]** 中所指定的空格數目。 如果 **[縮排大小]** 不是 **[定位點大小]** 的倍數，就會加入空格字元以填滿差異。  
  
  
