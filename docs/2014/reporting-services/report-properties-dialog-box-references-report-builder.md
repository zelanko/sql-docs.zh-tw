---
title: 報表屬性對話方塊、 參考 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 540ba2502ebf55b493c901640513f19382b22a37
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292786"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>報表屬性對話方塊、參考 (報表產生器)
  選取 **[報表屬性]** 對話方塊上的 **[參考]** ，即可將參考加入報表定義中運算式所使用的自訂或其他外部組件以及自訂類別執行個體，或從中移除。 在報表產生器的本機模式中不支援自訂組件。 若要撰寫使用自訂組件的報表，請使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的報表設計師。  
  
## <a name="options"></a>選項。  
 **新增或移除組件**  
 列出報表參考的組件。 組件必須可以在安裝設計報表所使用之工具的電腦和報表伺服器上使用。 參考的名稱必須符合的內容 **\<CodeModule >** 完全標記儲存在報表定義語言 (.rdl) 檔案。  
  
 **[加入]**  
 按一下即可加入組件。 按一下省略符號 （...） 按鈕，以開啟**開啟**對話方塊並選取完成報表處理和運算式評估所需的組件。  
  
 **移除**  
 若要從清單中移除組件參考，請選取組件名稱，再按一下 **[移除]** 按鈕。  
  
 **加入或移除類別**  
 列出報表所使用的類別執行個體。 類別清單僅供以執行個體為基礎的成員使用，並非供靜態成員使用。  
  
 **[加入]**  
 按一下即可加入類別參考。 按一下省略符號 （...） 按鈕，以開啟**開啟**對話方塊並選取完成報表處理和運算式評估所需的類別。  
  
 **移除**  
 若要刪除類別執行個體，請選取該執行個體，並按一下 **[移除]** 按鈕。  
  
 **向上**  
 若為具有相依性的類別，您可將這個參考移動至清單中的較高位置。  
  
 **向下**  
 若為具有相依性的類別，您可將這個參考移動至清單中的較低位置。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和精靈的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
