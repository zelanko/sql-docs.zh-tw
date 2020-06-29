---
title: 在資料流程元件中設定錯誤輸出 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- errors [Integration Services], data flow components
- components [Integration Services], data flow
- error outputs [Integration Services]
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6f5db0ec29fb6900dbe74ea021f31d0afc5551d7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434885"
---
# <a name="configure-an-error-output-in-a-data-flow-component"></a>在資料流程元件中設定錯誤輸出
  許多資料流程元件都支援錯誤輸出，因元件的不同， [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師會以不同的方式設定錯誤輸出。 除了設定錯誤輸出以外，您也可以設定錯誤輸出的資料行。 其中包括設定此元件所加入的 **ErrorCode** 和 **ErrorColumn** 資料行。  
  
## <a name="configuring-an-error-output"></a>設定錯誤輸出  
 若要設定錯誤輸出，您有兩個選項：  
  
-   使用 [設定錯誤輸出]**** 對話方塊。 您可以使用此對話方塊，在支援錯誤輸出的任何資料流程元件中設定錯誤輸出。  
  
-   請針對此元件使用編輯器對話方塊。 某些元件可讓您直接從它們的編輯器對話方塊設定錯誤輸出； 但如果是 ADO NET 來源、匯入資料行轉換、OLE DB 命令轉換或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 目的地，您便無法從編輯器對話方塊設定錯誤輸出。  
  
 下列程序描述如何使用這些對話方塊來設定錯誤輸出。  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>若要使用 [設定錯誤輸出] 對話方塊設定錯誤輸出  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [資料流程]**** 索引標籤。  
  
4.  將錯誤輸出 (以紅色箭頭表示) 從錯誤來源元件拖曳到資料流程中的另一個元件。  
  
5.  在 [設定錯誤輸出]**** 對話方塊中，針對元件輸入中的每個資料行，在 [錯誤]**** 和 [截斷]**** 資料行中選取動作。  
  
6.  若要儲存已更新的封裝，請按一下 [檔案]**** 功能表上的 [儲存選取項目]****。  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>針對此元件使用編輯器對話方塊來加入錯誤輸出  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [資料流程]**** 索引標籤。  
  
4.  按兩下要在其中設定錯誤輸出的資料流程元件，並依據此元件，執行下列其中一個步驟：  
  
    -   按一下 [設定錯誤輸出]****。  
  
    -   按一下 [錯誤輸出]****。  
  
5.  為每個資料行設定 [錯誤]**** 選項。  
  
6.  為每個資料行設定 [截斷]**** 選項。  
  
7.  按一下 [確定]****。  
  
8.  若要儲存已更新的封裝，請按一下 [檔案]**** 功能表上的 [儲存選取項目]****。  
  
## <a name="configuring-error-output-columns"></a>設定錯誤輸出資料行  
 若要設定錯誤輸出資料行，您必須使用 [進階編輯器]**** 對話方塊的 [輸入與輸出屬性]**** 索引標籤。  
  
#### <a name="to-configure-error-output-columns"></a>設定錯誤輸出資料行  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [資料流程]**** 索引標籤。  
  
4.  以滑鼠右鍵按一下要設定其錯誤輸出資料行的元件，並按一下 [顯示進階編輯器]****。  
  
5.  按一下 [**輸入和輸出屬性**] 索引標籤，然後展開 [ ** \<component name> 錯誤輸出**]，再展開 [**輸出資料行**]。  
  
6.  按一下資料行並更新其屬性。  
  
    > [!NOTE]  
    >  資料行的清單包括元件輸入中的資料行、上一個錯誤輸出加入的 **ErrorCode** 和 **ErrorColumn** 資料行，以及此元件加入的 **ErrorCode** 和 **ErrorColumn** 資料行。  
  
7.  按一下 [確定]   
  
8.  若要儲存已更新的封裝，請按一下 [檔案]**** 功能表上的 [儲存選取項目]****。  
  
## <a name="see-also"></a>另請參閱  
 [處理資料中的錯誤](data-flow/error-handling-in-data.md)  
  
  
