---
title: 選取巢狀的資料表索引鍵資料行對話方塊 （採礦結構檢視） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.structure.addnestedtable.f1
helpviewer_keywords:
- Select a Nested Table Key Column dialog box
ms.assetid: f68b89a7-17df-45f8-ba7f-b458cd9b1ec3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7eaccd916ee401ad1b6b82a155e50688b2ff57a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227533"
---
# <a name="select-a-nested-table-key-column-dialog-box-mining-structure-view"></a>選取巢狀資料表索引鍵資料行對話方塊 (採礦結構檢視)
  使用 **[選取巢狀資料表索引鍵資料行]** 對話方塊，即可指定將作為新巢狀資料表之索引鍵的資料行。 當您結束對話方塊時，會將新資料表加入至包含指定索引鍵資料行的採礦結構。 以滑鼠右鍵按一下結構，然後選取 [加入資料行]，即可將其他資料行加入至巢狀資料表。 視您正在處理 OLAP 採礦模型或是關聯式採礦模型而定，此對話方塊會包含不同的選項。  
  
## <a name="options"></a>選項。  
 **來源資料表**  
 作為採礦模型基礎的資料表。  
  
 這只用於關聯式採礦模型。  
  
 **來源資料行**  
 在來源資料表中，您可以用來作為巢狀資料表之索引鍵的所有可用資料行清單。  
  
 這只用於關聯式採礦模型。  
  
 **顯示資料行類型**  
 可用資料行資料類型的清單。 選取或清除資料類型，以篩選 **[來源資料行]** 中的資料行清單。 在 **[來源資料行]** 清單中，只會顯示與核取的資料類型相符的資料行。  
  
 這只用於關聯式採礦模型。  
  
 **屬性**  
 您可以用來作為巢狀資料表之索引鍵的屬性清單。  
  
 此選項只用於 OLAP 採礦模型。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構 檢視&#40;資料採礦模型設計工具&#41;](mining-structure-view-data-mining-model-designer.md)  
  
  
