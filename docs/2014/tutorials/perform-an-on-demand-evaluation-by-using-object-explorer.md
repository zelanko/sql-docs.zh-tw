---
title: 使用物件總管執行視需要評估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 95ce7493353fbce70ec10f575b7a637ea4d8809c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237928"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>使用物件總管執行視需要評估
  在這項工作中，您將使用 [物件總管]，針對 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的單一執行個體，為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行最佳作法原則的視需要評估。  
  
> [!NOTE]  
>  您也可以透過已註冊的伺服器評估單一執行個體的原則。 如需詳細資訊，請參閱 <<c0> [ 藉由使用已註冊的伺服器需要隨評估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)。  
  
## <a name="prerequisites"></a>先決條件  
 這一課是以 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本為基礎。  
  
> [!NOTE]  
>  若要執行對正在執行的執行個體的最佳作法原則的視需要評估[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，您必須使用此程序 > 主題中[執行所使用已註冊的伺服器隨評估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)。  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>若要使用物件總管執行視需要評估  
  
1.  啟動 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然後連接至 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在 [物件總管] 中，展開**管理**，展開**原則管理**，以滑鼠右鍵按一下**原則**，然後按一下**評估**。  
  
    > [!NOTE]  
    >  根據預設，本機執行個體會當做原則來源使用。 如果您先前已匯入最佳做法原則，則會列出這些原則以及您已經建立的其他所有原則。 您可以選取任何匯入的最佳做法原則，，然後按一下**Evaluate**。 如果您尚未匯入最佳做法原則，請繼續此程序。  
  
3.  在 [**評估原則**] 對話方塊中的 [下一步**來源**方塊中，按一下省略符號 (**...**)] 按鈕。  
  
4.  在 [**選取來源**] 對話方塊中，您可以選取**檔案**或**Server**做為評估之原則檔案的來源。 如果您按一下**Server**，您可以執行任何先前已匯入至本機或遠端伺服器上的原則式管理的最佳作法原則的視需要評估。 在本教學課程中，您不需要按**檔案**，然後選取您想要評估的個別原則檔案。 若要這樣做，請遵循下列步驟：  
  
    1.  按一下 **檔案**。  
  
    2.  旁**檔案**，按一下省略符號 (**...**) 按鈕。  
  
    3.  在 [**選取原則**] 對話方塊中，瀏覽至下列資料夾，其中包含最佳作法原則：  
  
         **C:\Program 檔案 (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  檔案路徑可能會隨著您安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程式檔案的位置、執行 32 位元或 64 位元作業系統，以及語言識別碼而有所不同。  
  
    4.  選取一或多個.xml 原則檔案來評估，然後按一下**開啟**。  
  
         選取的檔案清單會出現在**檔案** 方塊中。  
  
    5.  在 [**選取來源**] 對話方塊中，按一下**確定**。  
  
    6.  如果**正在載入原則** 對話方塊出現時，按一下**關閉**。  
  
     您選取的原則會列在**原則選取**頁面。 請注意，原則旁邊的警告圖示表示該原則包含指令碼。  
  
5.  按一下  **Evaluate**來評估原則。  
  
     在 **結果**資料表，結果會列出每個原則。 紅色的 "x" 圖示表示原則符合失敗。  
  
6.  對於某些原則失敗，以原則為基礎的管理可讓您立即強制符合目標上的原則。 若是此類失敗，失敗的原則旁邊會出現一個核取方塊。 如果您選取核取方塊中，**套用**按鈕會變成可用。 當您按一下 **套用**，不符合規範的設定將會自動更新目標執行個體上。  
  
    > [!CAUTION]  
    >  請在自動更新目標執行個體之前，確認您完全了解原則設定。 我們建議您選取一或多個核取方塊之後，您按一下**指令碼**，然後選擇 輸出位置，讓您可以檢閱基礎[!INCLUDE[tsql](../includes/tsql-md.md)]程式碼之前套用所做的變更。  
  
7.  若要檢視之原則的詳細的結果，請按一下 中的原則**結果**資料表。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [使用已註冊的伺服器執行隨選評估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
