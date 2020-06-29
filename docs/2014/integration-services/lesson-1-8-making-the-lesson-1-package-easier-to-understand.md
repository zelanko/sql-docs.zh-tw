---
title: 步驟 8：使第 1 課的封裝更容易了解 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e3a8837cbf3b102435a94706ee277aab9a42fb73
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440675"
---
# <a name="step-8-making-the-lesson-1-package-easier-to-understand"></a>步驟 8：使第 1 課的封裝更容易了解
  現在您已完成第 1 課封裝的組態，不妨整理一下封裝配置。 如果控制流程配置和資料流程配置中的形狀是隨機大小，或形狀沒有對齊或分組，則封裝功能可能更難以了解。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 會提供方便而快速格式化封裝配置的工具。 格式化功能包括使形狀變成相同大小、對齊形狀和操控形狀之間水平和垂直距離的能力。  
  
 進一步了解封裝的另一個方法是加入描述封裝功能的註解。  
  
 在這項工作中，您將使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 中的格式化功能來加強資料流程的配置，以及將註解加入資料流程中。  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>若要格式化資料流程的配置  
  
1.  如果第 1 課封裝尚未開啟，按兩下 [方案總管] 中的 Lesson 1.dtsx。  
  
2.  按一下 **[資料流程]** 索引標籤。  
  
3.  將資料指標放到 [擷取範例貨幣] 轉換的上面和右邊、按一下滑鼠按鍵，然後在所有資料流程元件上拖曳資料指標。  
  
4.  在 **[格式]** 功能表上，指向 **[設定成相同大小]**，再按一下 **[兩者]**。  
  
5.  選取資料流程物件之後，在 **[格式]** 功能表上，指向 **[對齊]**，然後按一下 **[靠左]**。  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>若要將註解加入資料流程中  
  
1.  以滑鼠右鍵按一下資料流程設計介面背景中的任何位置，然後按一下 **[加入註解]**。  
  
2.  在註解方塊中輸入或貼上下列文字。  
  
     **資料流程會從檔案中擷取資料，在 DimCurrency 資料表的 CurrencyKey 資料行和 DimDate 資料表的 DateKey 資料行中查閱值，然後將資料寫入至 NewFactCurrencyRate 資料表中。**  
  
     若要使註解方塊中的文字換行，請將游標放在您要開始新行的位置，然後按 Enter 鍵。  
  
     如果您沒有將文字加入註解方塊中，則您在方塊之外按一下時，它就會消失不見。  
  
## <a name="next-steps"></a>後續步驟  
 [步驟 9：測試第 1 課的教學課程封裝](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
