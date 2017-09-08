---
title: "定義資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5a3e83c9-8788-431e-85b0-a68c79377ff3
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c8256f6029efcb956e68325b134b72fcce452c8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-2---defining-a-data-source"></a>課程 1-2-定義資料來源
建立 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案之後，您通常會定義專案要使用的一或多個資料來源來開始使用專案。 當您定義資料來源時，要定義用來連接到資料來源的連接字串資訊。 如需詳細資訊，請參閱 [建立資料來源 &#40;SSAS 多維度&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)。  
  
在下列工作中，您會將 AdventureWorksDWSQLServer2012 範例資料庫定義為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案的資料來源。 基於這個教學課程的目的，這個資料庫是位於本機電腦上，而來源資料庫常常受主控於一部或多部遠端電腦上。  
  
### <a name="to-define-a-new-data-source"></a>若要定義新的資料來源  
  
1.  在方案總管中 (於 [Microsoft Visual Studio] 視窗右側)，以滑鼠右鍵按一下 [資料來源]，然後按一下 [新增資料來源]。  
  
2.  在**歡迎使用資料來源精靈**頁面**資料來源精靈**，按一下 **下一步**開啟**選取如何定義連接**頁面。  
  
3.  在 [選取如何定義連接] 頁面上，您可以根據新連接、現有的連接或先前定義的資料來源物件定義資料來源。 在此教學課程中，您將根據據新連接定義資料來源。 確認已選取 [依據現有的或新的連接建立資料來源]，然後按一下 [新增]。  
  
4.  在 [連線管理員] 對話方塊中，您可以定義資料來源的連線屬性。 在 [提供者] 清單方塊中，確認已選取 [Native OLE DB\SQL Server Native Client 11.0]。  
  
    [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]也支援其他提供者會顯示在**提供者**清單。  
  
5.  在 [伺服器名稱] 文字方塊中，輸入 **localhost**。  
  
    若要連接到本機電腦上的具名執行個體，輸入**localhost\\<instance name>**。 若要連接至特定電腦而非本機電腦，請輸入電腦名稱或 IP 位址。  
  
6.  確認已選取 [使用 Windows 驗證]。 在 [選取或輸入資料庫名稱] 清單中，選取 [AdventureWorksDW2012]。  
  
7.  按一下 [測試連接] 測試與伺服器的連接。  
  
8.  按一下 [確定]，然後按一下 [下一步]。  
  
9. 在精靈的 [模擬資訊] 頁面上，您可以定義 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用來連接到資料來源的安全性認證。 模擬會影響在選取 Windows 驗證時，用於連接至資料來源的 Windows 帳戶。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不支援模擬處理 OLAP 物件。 選取 [使用服務帳戶]，然後按一下 [下一步]。  
  
10. 在 [正在完成精靈] 頁面上，接受預設名稱 **Adventure Works DW 2012**，然後按一下 [完成] 來建立新的資料來源。  
  
> [!NOTE]  
> 若要在建立資料來源之後修改其屬性，請按兩下 [資料來源] 資料夾中的資料來源，以便在 [資料來源設計師] 中顯示資料來源屬性。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[定義資料來源檢視](../analysis-services/lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>另請參閱  
[建立資料來源 &#40;SSAS 多維度&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  

