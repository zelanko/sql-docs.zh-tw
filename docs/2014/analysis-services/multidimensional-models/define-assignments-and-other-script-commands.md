---
title: 定義指派和其他指令碼命令 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- empty scripts [Analysis Services]
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [Analysis Services], calculations
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e95dff588932bc7885d2501e3d24cc643ae10272
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699927"
---
# <a name="define-assignments-and-other-script-commands"></a>定義指派和其他指令碼命令
  在 [Cube 設計師] 的 [計算] 索引標籤上，按一下工具列上的**新增指令碼命令**圖示，來建立空的指令碼。 當您建立新的指令碼時，[計算] 索引標籤的 [指令碼組合管理] 窗格中，一開始會顯示空白的標題。您在 [計算運算式] 窗格中輸入的字元，會在 [指令碼組合管理] 中顯示為項目的名稱。 所以您可能想要在第一列輸入註解的名稱，以便更輕易地識別 [指令碼組合管理] 窗格中的指令碼。 如需詳細資訊，請參閱 [Introduction to MDX Scripting in Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892) (Microsoft SQL Server 2005 的 MDX 指令碼簡介)。 如需有關 MDX 查詢和計算相關效能問題的詳細資訊，請參閱 < 撰寫有效率的 MDX > 一節中[SQL Server 2005 Analysis Services 效能指南](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)。  
  
> [!IMPORTANT]  
>  當您最初切換到 [Cube 設計師] 的 [計算] 索引標籤時，[指令碼組合管理] 窗格會包含具有 CALCULATE 命令的單一指令碼。 唯有當您想要手動指定要如何彙總 Cube 時，CALCULATE 命令才會控制 Cube 中資料格的彙總，也才需要編輯。  
  
 您可以使用 [計算運算式] 窗格，來建立採用多維度運算式 (MDX) 語法的運算式。 當您建立運算式時，可以將 Cube 元件、函數以及範本，從 [計算工具] 窗格拖放或複製到 [計算運算式] 窗格。 此舉會將項目的指令碼加入 [計算運算式] 窗格中，您放下或貼上它的位置。 用適當的值來取代引數及其分隔符號 (« 和 »)。  
  
> [!IMPORTANT]  
>  當使用 [計算運算式] 窗格來撰寫包含多個陳述式的運算式時，請確定 MDX 指令碼的所有列 (除了最後一列之外) 都用分號 (;) 結束。 計算會串連成單一 MDX 指令碼，且每個指令碼都附加一個分號，以確定會正確編譯 MDX 指令碼。 如果您將分號加入 [計算運算式] 窗格中指令碼的最後一列，Cube 就會正確地建立及部署，但您將無法針對它執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [Calculations in Multidimensional Models](calculations-in-multidimensional-models.md)  
  
  
