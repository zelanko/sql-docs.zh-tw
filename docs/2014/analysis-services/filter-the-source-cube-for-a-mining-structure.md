---
title: 篩選採礦結構的來源 Cube |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed1ff70d4bb0f0ebd20da468c91f2603318ec217
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132761"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>篩選採礦結構的來源 Cube
  當您建立多維度模型 (OLAP cube) 中的資料為基礎的採礦結構時，您可以*配量*採礦結構為基礎的 cube。 配量處理可讓您建立資料子集，當做用來定型採礦模型的一種資料篩選。  
  
### <a name="to-slice-a-cube"></a>若要對 Cube 進行配量處理  
  
1.  資料採礦設計師中[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]，選取**採礦結構** 索引標籤或**採礦模型** 索引標籤。  
  
2.  在**採礦模型**功能表上，選取**定義採礦結構 Cube 配量**。  
  
     **配量 Cube**對話方塊隨即開啟。  
  
3.  在**維度**資料行**配量 Cube**對話方塊方塊中，選取您想要篩選的維度。  
  
4.  選取使用的清單中的階層層級**階層**資料行。  
  
5.  從清單中選取操作員**運算子**資料行，以用於建立篩選條件。  
  
6.  按一下此方塊中的**篩選**資料行。  
  
     隨即開啟一個對話方塊，其中包含指定之階層層級的所有成員。  
  
7.  選取您要篩選的成員。  
  
8.  按一下**確定**[成員] 對話方塊中。  
  
9. 按一下**確定**中**配量 Cube**  對話方塊。  
  
     來源 Cube 現在會依 Cube 配量定義來篩選。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和使用說明](data-mining/mining-structure-tasks-and-how-tos.md)   
 [建立新的 OLAP 採礦結構](data-mining/create-a-new-olap-mining-structure.md)  
  
  