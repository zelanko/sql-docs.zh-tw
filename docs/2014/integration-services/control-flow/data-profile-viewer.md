---
title: 資料設定檔檢視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0f6bcad3636178fb4aebbcdbeee29ba2542f092e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832413"
---
# <a name="data-profile-viewer"></a>資料設定檔檢視器
  檢視和分析資料設定檔是資料分析程序中的下一個步驟。 您可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝內部執行「資料分析」工作並計算資料設定檔後，檢視這些設定檔。 如需如何設定和執行「資料分析」工作的詳細資訊，請參閱 [資料分析工作的設定](data-profiling-task.md)。  
  
> [!IMPORTANT]  
>  輸出檔可能包含您資料庫的相關敏感性資料，以及資料庫所包含的資料。 如需如何讓這個檔案更安全的相關建議，請參閱 [對封裝使用之檔案的存取權](../access-to-files-used-by-packages.md)。  
  
## <a name="data-profiles"></a>資料設定檔  
 若要檢視資料設定檔，您可以設定「資料分析」工作，將其輸出傳送到檔案，然後使用獨立的「資料設定檔檢視器」即可。 若要開啟資料設定檔檢視器，請執行下列其中一項操作。  
  
-   以滑鼠右鍵按一下 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的 [資料分析]  工作，然後按一下 [編輯]  。 在 [資料分析工作編輯器]  的 [一般]  頁面上按一下 [開啟設定檔檢視器]  。  
  
-   在 \<磁碟機>  :\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn 資料夾中，執行 DataProfileViewer.exe。  
  
 此檢視器可使用多個窗格，顯示您所要求與計算之結果的設定檔以及選擇性的詳細資料與向下鑽研能力：  
  
 **設定檔**窗格  
 [設定檔]  窗格會顯示「資料設定檔」工作所要求的設定檔。 若要檢視設定檔的計算結果，請在 [設定檔]  窗格中選取設定檔，結果就會顯示在檢視器的其他窗格中。  
  
 **結果** 窗格  
 [結果]  窗格會使用單一資料列來摘要說明設定檔的計算結果。 例如，如果您要求 [資料行長度散發設定檔]  ，這個資料列會包含最小和最大長度，以及資料列計數。 對於大部分的設定檔，您可以在 [結果]  窗格中選取這個資料列，以便在選用的 [詳細資料]  窗格中查看其他詳細資料。  
  
 **詳細資料**窗格  
 對於大部分的設定檔類型，[詳細資料]  窗格會顯示在 [結果]  窗格中選取之設定檔結果的其他相關資訊。 例如，如果您要求 [資料行長度散發設定檔]  ，[詳細資料]  窗格會顯示所找到的每個資料行長度。 此窗格也會顯示資料行值中，具有該資料行長度之資料列的數目與百分比。  
  
 對於根據一個以上的資料行所計算的三種設定檔類型 ([候選索引鍵]、[功能相依性] 與 [值包含])，[詳細資料]  窗格會顯示預期關聯性的違規。 例如，如果您要求 [候選索引鍵設定檔]，[詳細資料] 窗格會顯示違反候選索引鍵唯一性的重複值。  
  
 如果可以使用計算設定檔所使用的資料來源，您可以在 [詳細資料]  窗格中按兩下資料列，以便在 [向下鑽研]  窗格中查看相符的資料列。  
  
 **向下鑽研**窗格  
 當以下條件成立時，您可以在 [詳細資料]  窗格中按兩下資料列，在 [向下鑽研]  窗格中查看相符的資料列：  
  
-   可以使用用來計算設定檔的資料來源。  
  
-   您具有檢視資料的權限。  
  
 為了連接到來源資料庫完成向下鑽研要求，資料設定檔檢視器會使用 Windows 驗證及目前使用者的認證。 資料設定檔檢視器不會使用儲存在執行「資料分析」工作之封裝內的連接資訊。  
  
> [!IMPORTANT]  
>  資料設定檔檢視器所提供的向下鑽研功能會傳送即時查詢給原始資料來源。 這些查詢對於伺服器的效能可能會有負面影響。  
>   
>  如果您從不是最近建立的輸出檔向下切入，則向下鑽研查詢傳回的資料列集可能與計算原始輸出的資料列集不同。  
  
 如需資料設定檔檢視器之使用者介面的詳細資訊，請參閱 [資料設定檔檢視器 F1 說明](../data-profile-viewer-f1-help.md)。  
  
  
