---
title: 將組件參考新增至報表 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 78e888c74c1bac7c3f4d26ae49e92dfdb3451874
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052260"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>將組件參考加入至報表 (SSRS)
  當您內嵌的自訂程式碼包含了不在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 或 <xref:System.Math> 中之 <xref:System.Convert>類別的參考時，您必須提供此報表的組件參考，好讓報表處理器可以解析名稱。 如需詳細資訊，請參閱[將程式碼加入至報表 &#40;SSRS&#41;](add-code-to-a-report-ssrs.md)。  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>若要將組件參考加入至報表  
  
1.  在 [設計] 檢視中，以滑鼠右鍵按一下報表框線外面的設計介面，然後按一下 [報表屬性]。  
  
2.  按一下 **[參考]**。  
  
3.  在 **[加入或移除組件]** 中，按一下 **[加入]** ，然後按一下省略符號按鈕，瀏覽至該組件。  
  
4.  在 **[加入或移除類別]** 中，按一下 **[加入]** ，然後輸入類別的名稱，再提供報表內所要使用的執行個體名稱。  
  
    > [!NOTE]  
    >  只針對以執行個體為基礎的成員，指定類別和執行個體名稱。 請勿指定 **[類別]** 清單中的靜態成員。 如需詳細資訊，請參閱[報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [與報表搭配使用自訂組件](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [報表屬性對話方塊、參考](../report-properties-dialog-box-references.md)  
  
  
