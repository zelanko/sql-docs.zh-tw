---
title: 工作 6：設定同義字 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 41c11138d00b4aea7332dac9984cbd609eba05e3
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489088"
---
# <a name="task-6-setting-synonyms"></a>工作 6：設定同義字
  在這個工作中，您可以設定兩個定義域值，**美國**並**美國**的**國家/地區**同義字的網域**美國**為前置值。 由於**使用前置值**建立時，已選取選項**國家/地區**網域中，任何**USA**值**國家/地區**網域將會輸出為**美國**（因為 United States 是前置值）。 請參閱[Change Domain Values](https://msdn.microsoft.com/library/hh510408.aspx)如需詳細資訊。  
  
1.  選取 **國家/地區**從網域清單。  
  
2.  若要切換**定義域值** 索引標籤。  
  
3.  按一下 **加入新的定義域值**工具列上的按鈕。  
  
4.  型別**USA**值並按下**ENTER**。  
  
5.  Multiselect**美國**並**USA**使用 CTRL 或 SHIFT 鍵，以滑鼠右鍵按一下選取的項目，然後**設為同義字**。 DQS 會將這些值分組在一起，並將其中一個值指定為將用來取代其他值的前置值。  
  
     ![設定為同義字 功能表](../../2014/tutorials/media/et-settingsynonyms-01.jpg "設為同義字 功能表")  
  
6.  請注意，**美國**設為前置值。 如果您希望 USA 成為前置值，您可以滑鼠右鍵按一下 USA，並選取**設為前置**選項。 本教學課程中，我們使用**美國**為前置值。  
  
     ![United States 和 USA 為同義字](../../2014/tutorials/media/et-settingsynonyms-02.jpg "United States 和 USA 為同義字")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 7:建立複合定義域](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  
