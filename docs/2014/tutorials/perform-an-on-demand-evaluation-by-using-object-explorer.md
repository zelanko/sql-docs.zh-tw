---
title: 使用物件總管執行隨選評估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: da56673e05c092c965554b76572ac3b0486d2110
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044164"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>使用物件總管執行視需要評估
  在這項工作中，您將使用 [物件總管]，針對 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的單一執行個體，為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行最佳作法原則的視需要評估。  
  
> [!NOTE]  
>  您也可以透過已註冊的伺服器評估單一執行個體的原則。 如需詳細資訊，請參閱[使用已註冊的伺服器執行隨選評估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
 這一課是以 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本為基礎。  
  
> [!NOTE]  
>  若要針對執行中的實例執行最佳作法原則的視需要評估 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ，您必須使用使用[已註冊的伺服器執行隨選評估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)主題中的程式。  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>若要使用物件總管執行視需要評估  
  
1.  啟動 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然後連接至 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在物件總管中，展開 [**管理**]，展開 [**原則管理**]，以滑鼠右鍵按一下 [**原則**]，然後按一下 [**評估**]。  
  
    > [!NOTE]  
    >  根據預設，本機執行個體會當做原則來源使用。 如果您先前已匯入最佳做法原則，則會列出這些原則以及您已經建立的其他所有原則。 您可以選取任何匯入的最佳做法原則，然後按一下 [**評估**]。 如果您尚未匯入最佳做法原則，請繼續此程序。  
  
3.  在 [**評估原則**] 對話方塊中，按一下 [**來源**] 方塊旁的省略號（**...**）按鈕。  
  
4.  在 [**選取來源**] 對話方塊中，您可以選取 [檔案 **] 或 [** **伺服器**] 做為要評估之原則檔案的來源。 如果您按一下 [**伺服器**]，可以針對先前匯入本機或遠端伺服器上以原則為基礎之管理的任何最佳作法原則，執行視需要評估。 在本教學課程**中，您將按一下 [** 檔案]，然後選取您想要評估的個別原則檔案。 若要這樣做，請遵循下列步驟：  
  
    1.  按一下 **[** 檔案]。  
  
    2.  在 [檔案]**旁，按一下**省略號（**...**）按鈕。  
  
    3.  在 [**選取原則**] 對話方塊中，流覽至包含最佳作法原則的下列資料夾：  
  
         **C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  檔案路徑可能會隨著您安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程式檔案的位置、執行 32 位元或 64 位元作業系統，以及語言識別碼而有所不同。  
  
    4.  選取一或多個要評估的 .xml 原則檔案，然後按一下 [**開啟**]。  
  
         選取的檔案清單會出現**在 [檔案**] 方塊中。  
  
    5.  在 [**選取來源**] 對話方塊中，按一下 **[確定]**。  
  
    6.  如果出現 [**正在載入原則**] 對話方塊，請按一下 [**關閉**]。  
  
     您選取的原則會列在 [**原則選取**] 頁面上。 請注意，原則旁邊的警告圖示表示該原則包含指令碼。  
  
5.  按一下 [**評估**] 以評估原則。  
  
     在 [**結果**] 資料表中，會列出每個原則的結果。 紅色的 "x" 圖示表示原則符合失敗。  
  
6.  對於某些原則失敗，以原則為基礎的管理可讓您立即強制符合目標上的原則。 若是此類失敗，失敗的原則旁邊會出現一個核取方塊。 如果您**選取此核取方塊，[套用**] 按鈕就會變成可用。 當**您按一下 [** 套用] 時，將會自動更新目標實例上不符合規範的設定。  
  
    > [!CAUTION]  
    >  請在自動更新目標執行個體之前，確認您完全了解原則設定。 我們建議您在選取一個或多個核取方塊後，按一下 [**腳本**]，然後選擇輸出位置，以便您可以在套用 [!INCLUDE[tsql](../includes/tsql-md.md)] 變更之前，先檢查基礎程式碼。  
  
7.  若要查看原則的詳細結果，請按一下 [**結果**] 資料表中的原則。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [使用已註冊的伺服器執行指定評估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
