---
title: "SQL Server Management Studio 中的使用者協助 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Help [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], user assistance
ms.assetid: 3c33a474-e507-4712-86fe-ae40e8370319
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c30d3be19643c13ba0621a948f3cca3b467cb039
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="user-assistance-in-sql-server-management-studio"></a>SQL Server Management Studio 中的使用者協助
您可以利用 [說明] 功能表和《 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 線上叢書》，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 中取得使用者輔助程式。 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 中的 [說明] 功能表提供了幾個不同的路徑，供您取得 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]的相關資訊。 您也可以利用它來存取 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 社群和 MSDN Online 資源，先前的 [說明] 環境並未提供這項功能。 另外，您現在也可以將 [說明] 環境設定成在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 環境內啟動，或在它自己的相關外部視窗中啟動。  
  
## <a name="the-help-interface"></a>說明介面  
[內容] 和 [索引] 提供類似於 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 使用者的功能和介面。 其他選項包括：  
  
-   **如何**  
  
    提供一組階層式連結頁面，頁面中含有對一般 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 工作非常有用的相關主題。 內容是依元件和工作來組織的，如＜複寫＞主題等。  
  
-   **搜尋**  
  
    搜尋主題，可以使用或不使用預先定義的篩選來搜尋。 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 中的 [搜尋] 是個別的索引標籤頁面。 使用者可以利用一或多個預先定義的主題類型、語言或技術篩選來修正他們的搜尋。 依預設，搜尋不會使用任何預先定義的篩選，只會搜尋已安裝之集合中的主題。  
  
    使用者可以啟用線上說明，將線上資源併入他們的搜尋中。 如需詳細資訊，請參閱這個主題稍後所提供的＜MSDN Online 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 社群＞。  
  
-   **動態說明**  
  
    當使用者在 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 環境中工作時，自動顯示相關資訊的連結。  
  
-   **最愛說明**  
  
    將使用者主題書籤儲存起來，以便日後方便存取。  
  
[如何使用輔助說明] \([!INCLUDE[msCoName](../includes/msconame_md.md)] Document Explorer 說明) 會將使用者連結到說明檢視器的相關文件集，但主題是在《[!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 線上叢書》以外的集合中。 如需有關說明檢視器的資訊，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 線上叢書》之 [說明] 功能表中的 [如何使用輔助說明]。  
  
## <a name="msdn-online-and-sql-server-communities"></a>MSDN Online 和 SQL Server 社群  
[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 中的說明也提供了若干方式，供使用者連絡 Web 中的 MSDN Online 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]焦點社群，以取得相關資訊。 您可以：  
  
-   從 [如何] 頁面中存取 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 社群。  
  
-   搜尋 MSDN Online 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 社群網站。  
  
#### <a name="to-access-sql-server-focused-communities-from-the-how-do-i-page"></a>從 [如何] 頁面存取 SQL Server 焦點社群  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 的 [說明] 功能表上，按一下 [如何]。  
  
2.  此時會開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 的 [如何] 頁面。 在 [社群連結] 提要欄位中，按一下您要存取的社群網站的名稱。  
  
    > [!NOTE]  
    > 執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 的電腦必須直接連接 Web。  
  
    在搜尋 MSDN Online 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 社群之前，您必須先啟用線上搜尋。  
  
#### <a name="to-enable-online-search"></a>啟用線上搜尋  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。 在 [選項] 對話方塊中，展開 [環境] 和 [說明] 節點 (必要的話)，再按一下 [線上]。  
  
2.  在 [載入說明內容時] 區域中，選取線上選項。  
  
3.  在 [搜尋這些提供者] 清單中，選取您要搜尋的搜尋提供者，並清除那些您不想要的提供者。  
  
4.  如果 [Codezone 社群] 是您選取的其中一個搜尋提供者，請在 [Codezone 社群] 清單中選取及清除適當的項目。  
  
5.  按一下 **[確定]**。  
  
#### <a name="to-search-msdn-online-and-sql-server-focused-communities-from-the-search-page"></a>從 [搜尋] 頁面搜尋 MSDN Online 和 SQL Server 焦點社群  
  
1.  在 [說明] 功能表上，按一下 [搜尋]。  
  
2.  在 [搜尋] 文字方塊中，輸入您的搜尋詞彙，再按一下 [搜尋]。  
  
不論您是否利用可用的篩選 (技術、語言和主題類型) 來執行搜尋，此時都會針對所有選取的搜尋提供者來執行您的搜尋。  
  
## <a name="launching-help"></a>啟動說明  
您可以從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]中，利用兩種方式來顯示 [說明]。 根據預設，從 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 內開啟《 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]線上叢書》時，它會在 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 環境之外的文件視窗中開啟。 這個視窗仍會關聯於 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]，它可以回應某些 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 事件，當您關閉 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]時，也會關閉線上叢書。 當您使用兩個監視器時，利用這個方式來開啟線上叢書，尤其有用；您可以在第一個監視器的工作之外，將 [線上叢書] 視窗拖曳至第二個監視器中，此時您仍可以輕易參考它。  
  
您也可以將線上叢書開啟成為 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]內的文件視窗。 當螢幕空間有限，且您想要利用 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 及其功能來隱藏視窗時，這個方式是您最佳的選擇。  
  
> [!NOTE]  
> 如果線上叢書要完全在 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 之外獨立運作，請從 [開始] 功能表中開啟《[!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 線上叢書》，它不會反應您在 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 環境中的動作，當您結束 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 時，也不會關閉它。  
  
#### <a name="to-configure-help-and-sql-server-books-online-to-launch-inside-the-management-studio-window"></a>設定在 [Management Studio] 視窗內啟動 [說明] 和《SQL Server 線上叢書》  
  
1.  在 [工具] 功能表上，按一下 [選項]、依序展開 [環境] 和 [說明]，再按一下 [一般]。  
  
2.  在 [顯示說明使用的工具] 方塊中，按一下 [整合式說明檢視器]。  
  
