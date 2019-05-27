---
title: 選項 （文字編輯器-Transact SQL 一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.General
dev_langs:
- TSQL
ms.assetid: 7021ecb7-8fb5-4d8c-b984-3d34fcde8be2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f32377fffb26ac622dc4045d108e491adc2b0342
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089164"
---
# <a name="options-text-editor---transact-sql--general-page"></a>選項 （文字編輯器-Transact SQL 一般頁面）
  使用 **[一般]** 選項對話方塊可以變更 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器的一般編輯行為，這個編輯器會用來編輯 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼。 若要顯示這些設定，請在 [工具] 功能表上按一下 [選項]，展開 [Transact-SQL] 子資料夾，然後按一下 [一般]。  
  
## <a name="setting-options-in-multiple-locations"></a>在多個位置設定選項  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器的選項也可以在 **[所有語言 - 一般]** 對話方塊中設定。 如果您使用 **[所有語言]** 對話方塊為其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 編輯器 (例如 DMX 或 MDX 編輯器) 設定不同的選項，則必須使用這個對話方塊重設 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器選項。  
  
## <a name="statement-completion"></a>陳述式完成  
 **自動列出成員**  
 選取此核取方塊時，當您在編輯器中輸入時將會顯示可用的資料庫和結構描述物件、資料行、資料表值函式或函數的清單。 從快顯清單擇取任何項目，以將其插入程式碼。  
  
 **隱藏進階成員**  
 無法使用此核取方塊。  
  
 **參數資訊**  
 如果選取此核取方塊，將會顯示緊接在插入點 (游標) 左邊之預存程序或函數的參數資訊。 此資訊包括可用參數的清單 (包含其名稱和資料類型)。  
  
## <a name="settings"></a>[設定]  
 **啟用虛擬空間**  
 選取這個核取方塊時，您可以按一下程式碼行結尾之外的任何位置，然後輸入內容。 選取此核取方塊，即可在程式碼旁的一致位置上放置註解。 選取這個核取方塊就會停用 **[自動換行]** 核取方塊。  
  
 **自動換行**  
 如果選取此核取方塊，超出可檢視的編輯器區域的行之任何部份，就會自動顯示在下一行。 選取此核取方塊會啟用 **[顯示自動換行的視覺化圖像]** 核取方塊並停用 **[啟用虛擬空間]** 核取方塊。  
  
 **顯示自動換行的視覺化圖像**  
 如果選取此核取方塊，就會顯示換行箭頭標記，其中過長的行就會自動換行到下一行。  
  
 **沒有選取項目時，套用剪下/複製命令至空白行**  
 當您在空白行上放置插入點、不選取任何內容，然後按一下 **[複製]** 或 **[剪下]** 時，此核取方塊就會設定編輯器的行為。  
  
 如果選取此核取方塊，就會複製或剪下空白行。 接著，如果您按一下 **[貼上]**，就會插入一個新的空白行。  
  
 如果清除此核取方塊，就不會複製或剪下任何內容。 接著，您按一下 **[貼上]**，就會貼上最近複製的內容。 如果先前沒有進行複製，就不會有貼上動作。  
  
 當行不是空白時，此設定對 **[複製]** 或 **[剪下]** 沒有影響。 如果沒有選取內容，就會複製或剪下整個行。 接著，如果您按一下 **[貼上]**，就會貼上整行的文字與其結束字元。  
  
## <a name="display"></a>顯示器  
 **行號**  
 如果選取此核取方塊，行號就會出現在每一行程式碼的旁邊。  
  
> [!NOTE]  
>  這些行號不會加入您的程式碼中，且不會列印。 它們僅供參考。  
  
 **啟用按一下方式的 URL 導覽**  
 如果選取此核取方塊，當游標在編輯器中的 URL 上方時會變成手指符號。 按一下 URL 即可在 Web 瀏覽器中顯示該頁面。  
  
 **導覽列**  
 無法使用此核取方塊。  
  
  
