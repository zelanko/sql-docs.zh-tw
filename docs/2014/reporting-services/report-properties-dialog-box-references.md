---
title: 報表屬性對話方塊、 參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3c6d90ae9945e7014158916df0ec5e04f03a6541
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59971344"
---
# <a name="report-properties-dialog-box-references"></a>報表屬性對話方塊、參考
  選取 **[報表屬性]** 對話方塊上的 **[參考]** ，即可將參考加入報表定義中運算式所使用的自訂或其他外部組件以及自訂類別執行個體，或從中移除。  
  
## <a name="options"></a>選項。  
 **新增或移除組件**  
 列出報表參考的組件。 組件必須可以在安裝設計報表所使用之工具的電腦和報表伺服器上使用。 參考的名稱必須符合的內容 **\<CodeModule >** 完全標記儲存在報表定義語言 (.rdl) 檔案。  
  
 **[加入]**  
 按一下即可加入組件。 按一下省略符號 （...） 按鈕，以開啟**開啟**對話方塊並選取完成報表處理和運算式評估所需的組件。  
  
 **刪除**  
 若要從清單中移除組件參考，請選取組件名稱，再按一下 **[移除]** 按鈕。  
  
 **加入或移除類別**  
 列出報表所使用的類別執行個體。 類別清單僅供以執行個體為基礎的成員使用，並非供靜態成員使用。  
  
 **[加入]**  
 按一下即可加入類別參考。 按一下省略符號 （...） 按鈕，以開啟**開啟**對話方塊並選取完成報表處理和運算式評估所需的類別。  
  
 **刪除**  
 若要刪除類別執行個體，請選取該執行個體，並按一下 **[移除]** 按鈕。  
  
 **向上**  
 若為具有相依性的類別，您可將這個參考移動至清單中的較高位置。  
  
 **向下**  
 若為具有相依性的類別，您可將這個參考移動至清單中的較低位置。  
  
## <a name="see-also"></a>另請參閱  
 [報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
