---
title: 在 Management Studio 中建立 Analysis Services 腳本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e3cca216f7c2312b4e7b54f2236a5d1f7bafd9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080105"
---
# <a name="create-analysis-services-scripts-in-management-studio"></a>在 Management Studio 中建立 Analysis Services 指令碼
  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包含指令碼產生功能、範本和編輯器，您可以使用它們來編寫 Analysis Services 物件和工作的指令碼。  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>在 Management Studio 中編寫 Analysis Services 工作的指令碼  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中編寫工作指令碼，是在工作導向的對話方塊中按一下其中一個指令碼選項來完成。 用來執行備份或還原資料庫、處理物件或設計彙總等工作的所有對話方塊，在對話方塊頂端都包含指令碼選項。 選取其中一個選項，會根據對話方塊中的資訊和設定來產生 XMLA 指令碼。  
  
 根據預設，產生的指令碼放在 XMLA 查詢編輯器中，但您也可以展開指令碼選項清單，將指令碼導向至 Windows 剪貼簿或檔案。  
  
#### <a name="to-script-an-analysis-services-task"></a>若要編寫 Analysis Services 工作的指令碼  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。  
  
2.  以滑鼠右鍵按一下資料庫，然後按一下 [備份]****。 這會開啟 [備份資料庫] 對話方塊。 指定備份檔案的名稱，並選擇要用於此備份的選項。  
  
3.  按一下對話方塊頂端的 [指令碼]****。 指令碼功能是 Management Studio 中所有以工作為基礎的對話方塊的一部分。 它有下列選項：[編寫動作的指令碼至新增查詢視窗]**** 可開啟查詢編輯器視窗、[編寫動作的指令碼至檔案]**** 可將 XMLA 指令碼儲存至檔案，或 [編寫動作的指令碼至剪貼簿]**** 可將 XMLA 指令碼儲存至剪貼簿。  
  
     請注意，Analysis Services 指令碼不支援 Management Studio 中列為指令碼選項的 [編寫動作的指令碼至作業]**** 選項。  
  
4.  如果您選取預設選項 [編寫動作的指令碼至新增查詢視窗]****，產生的指令碼會放在 XMLA 查詢視窗中。  
  
     您現在可以關閉 [備份資料庫] 對話方塊，然後編輯或直接執行 XMLA 指令碼。  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>在 Management Studio 中編寫 Analysis Services 物件的指令碼  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中編寫物件指令碼，是在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中以滑鼠右鍵按一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件，然後選取 [CREATE 至]****、[ALTER 至]**** 或 [DELETE 至]**** 來完成。 每一個這些選項可引導至視窗或檔案，但不論指令碼引導至何處，它將以 DDL 指令碼格式出現在 XMLA 包裝函數中。 這類指令碼的一大好處，就是它們可以對任何您指向的伺服器執行。 同時，可針對物件的大量建構、改變或刪除來反覆變更及執行指令碼的名稱。  
  
 可編寫指令碼的物件包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的元素，包含資料來源、資料來源檢視、Cube、維度、採礦結構和角色。  
  
 必要條件包含了解 XML for Analysis (XMLA)。 幸好 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 有自動建立 XMLA 指令碼的功能，可用來建立 Cube 等物件。 此自動化功能有助於縮短 XMLA 的學習曲線。 如需如何使用 XMLA 的詳細資訊，請參閱 [在 Analysis Services 中使用 XMLA 進行開發](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。 如需如何使用 XMLA 的詳細資訊，請參閱 [在 Analysis Services 中使用 XMLA 進行開發](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。  
  
> [!IMPORTANT]  
>  編寫 Role 物件的指令碼時，請注意安全性權限包含在它們所保護的物件中，而非與它們相關聯的安全性角色。  
  
#### <a name="to-script-analysis-services-objects"></a>若要編寫 Analysis Services 物件的指令碼  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。  
  
2.  尋找您要建立指令碼的物件，來建立、改變或刪除物件。  
  
3.  以滑鼠右鍵按一下物件，指向 [編寫 Cube 的指令碼為]****，然後指向 [CREATE 至]****、[ALTER 至]**** 或 [DELETE 至]****，再按下列其中一個選項：[新增查詢編輯器視窗]**** 可開啟查詢編輯器視窗、[檔案]**** 可將 XMLA 指令碼儲存至檔案，或 [剪貼簿]**** 可將 XMLA 指令碼儲存至剪貼簿。  
  
    > [!NOTE]  
    >  一般而言，如果您要建立檔案的多個不同版本，請選取 [檔案]****。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中編寫管理工作的腳本](../script-administrative-tasks-in-analysis-services.md)   
 [XMLA 查詢編輯器 &#40;Analysis Services-多維度資料&#41;](../xmla-query-editor-analysis-services-multidimensional-data.md)  
  
  
