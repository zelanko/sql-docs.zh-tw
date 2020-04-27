---
title: 篩選採礦結構的來源 Cube |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74220f2385e27484c5cc511c84be5625290a28db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081153"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>篩選採礦結構的來源 Cube
  當您建立以多維度模型中的資料為基礎的「採礦結構」（OLAP Cube）時，*您可以配*量此採礦結構所依據的 cube。 配量處理可讓您建立資料子集，當做用來定型採礦模型的一種資料篩選。  
  
### <a name="to-slice-a-cube"></a>若要對 Cube 進行配量處理  
  
1.  在的 [資料採礦[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]設計師] 中，選取 [**採礦結構**] 索引標籤或 [**採礦模型**] 索引標籤。  
  
2.  在 [**採礦模型**] 功能表上，選取 [**定義採礦結構 Cube**配量]。  
  
     [配量**Cube** ] 對話方塊隨即開啟。  
  
3.  在 [配量 Cube] 對話方塊的 [**維度**]**資料**行中，選取您要篩選的維度。  
  
4.  使用 [階層]**資料行中的清單**選取階層的層級。  
  
5.  從 [**運算子**] 資料行的清單中選取運算子，以用於建立篩選準則。  
  
6.  按一下 [**篩選**] 資料行中的方塊。  
  
     隨即開啟一個對話方塊，其中包含指定之階層層級的所有成員。  
  
7.  選取您要篩選的成員。  
  
8.  在 [成員] 對話方塊中按一下 **[確定]** 。  
  
9. 在 [配量**Cube** ] 對話方塊中，按一下 **[確定]** 。  
  
     來源 Cube 現在會依 Cube 配量定義來篩選。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和操作說明](data-mining/mining-structure-tasks-and-how-tos.md)   
 [建立新的 OLAP 採礦結構](data-mining/create-a-new-olap-mining-structure.md)  
  
  
