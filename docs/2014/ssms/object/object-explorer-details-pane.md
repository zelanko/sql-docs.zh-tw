---
title: 物件總管詳細資料窗格 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.summary.report.f1
- sql12.swb.summary.general.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 579316f5a919184528b70f3fb287f8cbe1711306
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815044"
---
# <a name="object-explorer-details-pane"></a>物件總管詳細資料窗格
  [物件總管詳細資料] 是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的元件，它會提供伺服器中所有物件的表格式檢視，並且呈現可管理這些物件的使用者介面。 物件總管的功能會隨著伺服器的類型而稍有不同，不過，它通常會包括資料庫的開發功能，以及所有伺服器類型的管理功能。  
  
 根據預設，[物件總管詳細資料] 窗格會顯示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中。 如果您看不到物件總管，請在 [檢視] 功能表上，按一下 [物件總管詳細資料] 或按下 **F7**。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會呈現利用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 啟動時在作用中的 Microsoft Windows [地區及語言選項] 所格式化的日期。 請重新啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來反映較新的設定。  
  
## <a name="object-explorer-details"></a>物件總管詳細資料  
 [物件總管詳細資料] 可用於逐一導覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的資料夾和物件。 在 32 位元作業系統上，[物件總管] 只能顯示 64,000 個物件。 您必須選取一個圖示來存取其他物件。  
  
 [物件總管詳細資料] 包括含有下表所述之圖示的工具列。 這些圖示只有在適當情況下才能使用。  
  
|圖示|動作|  
|----------|------------|  
|**上一頁**|移至 [物件總管詳細資料] 中顯示的先前項目。 當先前的顯示是搜尋作業的結果時，就會重新執行搜尋。|  
|**下一頁**|在選取 [上一頁] 作業之後，移至下一個畫面。|  
|**向上**|移至父物件或資料夾。|  
|**同步處理**|將 [物件總管] 的焦點設定成在 [物件總管詳細資料] 中選取的物件。|  
|**篩選**|如果可用，顯示可設定的物件子集。|  
|**[重新整理]**|重新整理 [物件總管詳細資料] 的顯示。|  
|**搜尋**|提供區域來輸入特定資料庫物件的搜尋詞彙。|  
  
### <a name="column-header-selections"></a>資料行標頭選取範圍  
 [物件總管詳細資料] 具有可選取的資料行。 您可以在任何資料行標頭中按一下滑鼠右鍵，然後檢查想要顯示的項目。 您的選取範圍將會保存在逐一導覽的不同物件中。 當您離開並重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]時，系統就會保留每位使用者的選取範圍。  
  
> [!CAUTION]  
>  若為大型物件集，顯示某些物件類型 (例如資料庫) 的所有資料行可能會稍微降低顯示轉譯的速度。  
  
### <a name="sorting"></a>排序  
 按一下資料行標頭就會依據該資料行進行排序。 再次按一下相同的標頭則會依據該資料行進行反向排序。 每位使用者的排序選取範圍會保留在物件和資料夾中，而且會在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 重新啟動時保留。  
  
### <a name="filtering"></a>篩選  
 您可以使用 [物件總管詳細資料] 工具列上的 [篩選] 圖示來篩選顯示在 [物件總管詳細資料] 中的特定物件清單。 此圖示會在可進行篩選時啟用。  
  
### <a name="details-pane"></a>詳細資料窗格  
 [物件總管詳細資料] 的最底部區域包含一個面板，其中顯示所選物件的特定詳細資料。 多重物件選取範圍只會顯示物件的計數。 在此面板中選取項目時，按一下 [複製] 圖示，即可將顯示的文字複製到 [剪貼簿]。  
  
 向下鍵會將選取範圍移至清單中的下一個項目。 向上鍵會將選取範圍移至清單中的上一個項目。 按住方向鍵則會加快在項目之間移動的速度。 選取範圍會在屬性清單的底部或頂端停止。  
  
 輸入屬性名稱的第一個字元就會將選取範圍移至以該字元為開頭的下一個屬性。  
  
 當屬性排列於多個欄位時，請使用向左鍵和向右鍵來移至相鄰的欄位。  
  
 若要將屬性值複製到 [剪貼簿]，請使用下列鍵盤組合鍵：  
  
-   Ctrl+C 會複製屬性值。  
  
-   Ctrl+Shift+C 會使用 Tab 鍵分隔符號來複製屬性名稱和屬性值。  
  
 您可以使用 [物件總管詳細資料] 屬性窗格中的右鍵功能表，將所有屬性或所有屬性和名稱複製到 [剪貼簿]。  
  
 若要在欄位寬度無法完全顯示屬性值時顯示屬性值，請將滑鼠游標停留在該值上方，或將 UI 焦點設定於該屬性值，以便啟動包含整個屬性值的工具提示。 當使用者將焦點設為冗長的屬性值時，協助工具螢幕助讀員將報告完整的屬性值。  
  
 如果屬性窗格中的屬性數目超過內容區域可容納的數目，屬性窗格的右側就會顯示捲軸。 您可以使用捲軸來調整內容區域中屬性值的檢視。  
  
### <a name="multiple-object-selection"></a>多重物件選取範圍  
 [物件總管詳細資料] 支援多重物件選取範圍。 例如，如果您在物件總管中選取 [資料表]，接著在 [物件總管詳細資料] 視窗中按住 **Ctrl** 鍵，就可以選取多個資料表、以滑鼠右鍵按一下它們，然後選取 [刪除] 或 [編寫資料表的指令碼為]，立即在所有選取的資料表上運作。 標準的複製命令會將顯示的文字複製到 [剪貼簿]。  
  
## <a name="sql-server-object-search"></a>SQL Server 物件搜尋  
 萬用字元  
  
-   支援標準的萬用字元。 例如，搜尋 **dm_os%counters** 就會傳回 dm_os_memory_cache_counters 和 dm_os_performance_counters。 如需詳細資訊，請參閱 <<c0> [ 使用萬用字元搜尋文字](../../relational-databases/scripting/search-text-with-wildcards.md)。  
  
 搜尋範圍  
  
-   每個搜尋的範圍都會設定成 [物件總管] 樹狀結構中的目前焦點。 例如，如果物件總管的焦點是資料庫，則搜尋 **dm_os%counters** 就會傳回該資料庫中的 dm_os_memory_cache_counters 和 dm_os_performance_counters。 如果 [物件總管] 的焦點是 [資料庫] 節點，就會搜尋所有資料庫，而且會傳回多個動態檢視的執行個體。  
  
 大型集  
  
-   搜尋大型物件集可能會需要很長的時間，而且會降低伺服器效能。  
  
## <a name="see-also"></a>另請參閱  
 [物件總管](object-explorer.md)  
  
  
