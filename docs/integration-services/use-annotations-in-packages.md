---
title: "在封裝中使用註釋 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- self-documenting packages
- adding annotations
- annotations [Integration Services]
ms.assetid: 48c8ed9a-b10d-490c-9ba7-4b77aa44e3dd
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dabeecf1a4e2715bf4ccd214ac21ff3311f27411
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="use-annotations-in-packages"></a>使用封裝中的註解
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師會提供註解，可用於使封裝自我記錄並易於了解及維護。 您可以將註解加入「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」的控制流程、資料流程及事件處理常式設計介面。 註解 (Annotation) 可以包含任何類型的文字，而且它們可用於將標籤、註解 (Comment) 及其他描述性資訊加入至封裝。 註解只是設計階段功能。 例如，註解不寫入記錄檔中。  
  
 當您按 ENTER 鍵時，文字會折行。 註解方塊會自動在您加入其他文字行時放大。 封裝註解會以純文字格式保存在封裝檔案的 CDATA 區段中。  
  
 如需對封裝檔案格式所做變更的詳細資訊，請參閱 [SSIS 封裝格式](http://msdn.microsoft.com/library/cfe0e5dc-5be3-4222-b721-fe83665edd94)。  
  
 當您儲存封裝時，「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」會在封裝中儲存註解。  
  
## <a name="add-an-annotation-to-a-package"></a>將註解加入封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要加入註解之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，以滑鼠右鍵按一下 [控制流程]、[資料流程] 或 [事件處理常式] 索引標籤設計介面上的任何位置，然後按一下 [加入註解]。 索引標籤的設計介面上將出現一個文字區塊。  
  
4.  加入文字。  
  
    > [!NOTE]  
    >  如果不加入文字，則按一下區塊以外的位置，文字區塊便會移除。  
  
5.  若要變更註解中文字的大小或格式，請在註解按一下滑鼠右鍵，然後選取 [設定文字註解的字型]。  
  
6.  若要加入其他文字行，請按 ENTER。  
  
     註解方塊會自動在您加入其他文字行時放大。  
  
7.  若要將註解加入群組，請在註解上按一下滑鼠右鍵，然後按一下 [群組]。  
  
8.  若要儲存更新的封裝，請按一下 **[檔案]** 功能表上的 **[全部儲存]**。  

