---
title: 將組件參考新增至報表 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
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
ms.openlocfilehash: c9725d51c934172c6c6291b6a7f1592a3ddc057c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080677"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>將組件參考加入至報表 (SSRS)
  當您內嵌的自訂程式碼包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別的參考，而該類別不在 <xref:System.Math> 或 <xref:System.Convert> 中時，則必須提供此報表的組件參考以讓報表處理器可以解析名稱。 如需詳細資訊，請參閱[將程式碼加入至報表 &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)。  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>若要將組件參考加入至報表  
  
1.  在 [設計]  檢視中，以滑鼠右鍵按一下報表框線外面的設計介面，然後按一下 [報表屬性]  。  
  
2.  按一下 **[參考]** 。  
  
3.  在 **[加入或移除組件]** 中，按一下 **[加入]** ，然後按一下省略符號按鈕，瀏覽至該組件。  
  
4.  在 **[加入或移除類別]** 中，按一下 **[加入]** ，然後輸入類別的名稱，再提供報表內所要使用的執行個體名稱。  
  
    > [!NOTE]  
    >  只針對以執行個體為基礎的成員，指定類別和執行個體名稱。 請勿指定 **[類別]** 清單中的靜態成員。 如需詳細資訊，請參閱 [報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [報表屬性對話方塊、參考](https://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
