---
title: 選項 （文字編輯器的 XML 格式化頁面） |Microsoft 文件
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
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5d77f7351d712f63e9cfc92c3ff03b131cb6d5d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023843"
---
# <a name="options-text-editor---xml---formatting-page"></a>選項 (文字編輯器 - XML - 格式化頁面)
  此對話方塊允許您指定 XML 編輯器的格式化設定。 您可以從 [工具] 功能表存取 [選項] 對話方塊。  
  
> [!NOTE]  
>  在選取 [文字編輯器] 資料夾、[XML] 資料夾，然後從 [選項] 對話方塊中選取 [格式化] 選項時，均可以使用這些設定。  
  
## <a name="attributes"></a>屬性  
 **保留手動屬性格式化**  
 不要重新格式化屬性。 這是預設值。  
  
> [!NOTE]  
>  如果屬性在多行中，編輯器就會縮排每一個屬性行，以符合父元素的縮排。  
  
 **將每一個屬性的個別行上對齊**  
 將第二個和後續的屬性垂直對齊，以符合第一個屬性的縮排。 下列 XML 文字是如何對齊屬性的範例。  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>自動重新格式化  
 **在從剪貼簿貼上。**  
 重新格式化從剪貼簿貼上的 XML 文字。  
  
 **完成結束標記**  
 完成結束標記時重新格式化元素。  
  
## <a name="mixed-content"></a>混合內容  
 **依預設，格式化混合的內容。**  
 嘗試重新格式化混合內容，但是在 `xml:space="preserve"` 範圍中找到的內容除外。 這是預設值。  
  
 如果元素包含文字與標記的混合，則內容會被視為混合內容。 下列是具有混合內容之元素的範例。  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</dir >  
  
## <a name="see-also"></a>另請參閱  
 [XML 編輯器 &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)  
  
  