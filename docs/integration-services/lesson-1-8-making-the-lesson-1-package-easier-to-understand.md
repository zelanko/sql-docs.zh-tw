---
title: 步驟 8：為第 1 課套件加上註解並設定格式 | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fffa5eed608e8cd3faeb13b084e15554e4a8092f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729409"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>課程 1-8：為第 1 課套件加上註解並設定格式 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



既然您已完成第 1 課套件的設定，現在或許是整理套件配置的好時機。 如果控制流程配置與資料流程配置中的形狀大小不同，或形狀沒有平均配置，就會更難以理解套件。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 提供可輕鬆設定套件配置格式的工具。 格式設定功能包括能夠讓形狀變成相同大小、讓形狀對齊，以及變更形狀之間的水平和垂直間距。  
  
進一步了解封裝的另一個方法是加入描述封裝功能的註解。  
  
在此工作中，您會使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 中的格式設定功能來改善資料流程的配置，以及新增註解。  
  
## <a name="format-the-layout-of-the-data-flow"></a>設定資料流程配置的格式  
  
1.  如果第 1 課套件尚未開啟，請按兩下 [方案總管] 中的 [Lesson 1.dtsx]。  
  
2.  選取 [資料流程] 索引標籤。  
  
3.  若要一次選取所有資料流程元件，請使用 [編輯] > [全選]。
  
4.  在 **[格式]** 功能表上，選取 [設定成相同大小]，然後選取 [兩者]。  
  
5.  選取資料流程物件之後，在 [格式] 功能表上，選取 [對齊]，然後選取 [置中]。  

6.  選取資料流程物件之後，在 [格式] 功能表上，指向 [垂直間距]，然後選取 [設成相等]。  
  
## <a name="add-an-annotation-to-the-data-flow"></a>將註解新增至資料流程  
  
1.  在資料流程設計介面背景中的任何位置按一下滑鼠右鍵，然後選取 [加入註解]。  
  
2.  在註解方塊中輸入或貼上下列文字。  
  
    資料流程會從檔案中擷取資料，在 DimCurrency 資料表的 CurrencyKey 資料行和 DimDate 資料表的 DateKey 資料行中查閱值，然後將資料寫入至 NewFactCurrencyRate 資料表中。
  
    若要讓註解方塊中的文字換行，請將游標放在您要開始新行的位置，然後按 **Enter** 鍵。  
  
    如果您沒有在註解方塊中新增文字，當您在方塊外按一下時，方塊就會消失。  由於此行為，如果您要在選取 [新增註解] 之前於註解方塊中貼上文字，然後複製文字到剪貼簿。 
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 9：測試第 1 課套件](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
