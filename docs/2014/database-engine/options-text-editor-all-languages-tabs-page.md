---
title: 選項 (文字編輯器-所有語言-定位點頁面) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
ms.assetid: bd715d6b-f873-41d4-aa10-57b7098b61cc
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2cc5922ed04933dcb7a6b09995353e7fd64a3163
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287854"
---
# <a name="options-text-editor---all-languages--tabs-page"></a>選項 (文字編輯器-所有語言-定位點頁面)
  使用這個對話方塊可設定在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的全部五個編輯器中按下 Tab 鍵的移動行為。 若要顯示這些選項，請按一下 [工具] 功能表上的 [選項]。 選取 [文字編輯器] 資料夾，展開 [所有語言] 資料夾，然後按一下 [索引標籤]。  
  
## <a name="tabbing-options-by-editor"></a>依編輯器的 Tab 鍵移動選項  
 您必須使用 [所有語言] 對話方塊設定 DMX、MDX 和 SQL Server Compact 編輯器的選項。 在此處設定的選項也會套用至純文字、Transact-SQL 和 XML 編輯器，不過，藉由展開這些語言的子資料夾，然後選取其選項頁面，您就可以個別為這些編輯器設定選項。 某些語言不支援所有 Tab 鍵移動選項。  
  
> [!CAUTION]  
>  如果您使用這個對話方塊設定選項，但是想要為純文字、Transact-SQL 或 XML 編輯器進行不同的設定，則必須先在 [所有語言] 對話方塊中套用您的選取範圍，再設定這些編輯器的選項。  
  
 當您為特定編輯器選取不同設定時，會顯示「個別文字格式的縮排 (或 Tab) 設定相衝突」訊息。 例如，如果針對 [純文字] 選取 [Block indenting (封鎖縮排)] 選項，而針對 [XML] 選取 [無]，就會顯示此提醒。  
  
## <a name="indenting"></a>縮排  
 **無**  
 如果選取此選項，當您按下 ENTER 時所建立的新行就不會縮排。 資料指標會放在新行的第一個資料行上。  
  
 **區塊**  
 如果選取此選項，當您按下 ENTER 鍵時所建立的新行就會自動縮排與上一行縮排相同的距離。  
  
 **智慧**  
 如果選取此選項，當您按下 ENTER 時所建立之新行的位置，就會根據內容而定。  
  
## <a name="tabs"></a>定位點  
 **定位點大小**  
 以空格數目，設定各定位點之間的距離。 預設值為四個空格。  
  
 **縮排大小**  
 以空格數目，設定自動縮排的大小。 預設值為四個空格。 將會插入定位字元、空格字元或兩者，以填滿指定的大小。  
  
 **插入空格**  
 如果選取此選項，縮排作業僅會插入空格字元，而非定位字元。 例如，若 [縮排大小] 設定為 5，在您按下 TAB 鍵或在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 主視窗的工具列上按一下 [增加縮排] 按鈕時，就會插入五個空格字元。  
  
 **保留定位點**  
 如果選取此選項，縮排作業會儘可能插入最多的定位字元。 每個定位字元會填滿 **[定位點大小]** 中所指定的空格數目。 如果 **[縮排大小]** 不是 **[定位點大小]** 的倍數，就會加入空格字元以填滿差異。  
  
  
