---
title: 使用合併聯結轉換來擴充資料集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8009dcd369327941004fe220782c38d5602b4dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62900300"
---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>使用合併聯結轉換來擴充資料集
  若要加入和設定「合併聯結」轉換，封裝必須已包含至少一個「資料流程」工作，及兩個為「合併聯結」轉換提供輸入的資料流程元件。  
  
 「合併聯結」轉換需要兩個經過排序的輸入。 如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
### <a name="to-extend-a-dataset"></a>擴充資料集  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [資料流程]  索引標籤，然後將「合併聯結」轉換從 [工具箱]  拖曳至設計介面。  
  
4.  將連接子從資料來源或前一個轉換拖曳至「合併聯結」轉換，以便將「合併聯結」轉換連接到資料流程。  
  
5.  按兩下「合併聯結」轉換。  
  
6.  在 [合併聯結轉換編輯器]  對話方塊中，選取 [聯結類型]  清單中使用的聯結類型。  
  
    > [!NOTE]  
    >  如果您選取 [左方外部聯結]  類型，則可以按一下 [交換輸入]  來切換輸入，並將左方外部聯結轉換成右方外部聯結。  
  
7.  將左輸入中的資料行拖曳至右輸入中的資料行，以指定聯結資料行。 如果這些資料行的名稱相同，則可以選取 [聯結索引鍵]  核取方塊，「合併聯結」轉換會自動建立聯結。  
  
    > [!NOTE]  
    >  您可以只在排序位置相同的資料行之間建立聯結，而這些聯結必須以排序位置指定的順序建立。 如果您嘗試不按順序建立聯結，則 [合併聯結轉換編輯器]  會提示您為略過的排序次序位置建立其他聯結。  
  
    > [!NOTE]  
    >  依預設，輸出會在聯結資料行上進行排序。  
  
8.  在左右輸入中，選取其他資料行的核取方塊，使之包含在輸出中。 依預設，會包含聯結資料行。  
  
9. (選擇性) 在 [輸出別名]  資料行中更新輸出資料行的名稱。  
  
10. 按一下 [確定]  。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [合併聯結轉換](merge-join-transformation.md)   
 [Integration Services 轉換](integration-services-transformations.md)   
 [Integration Services 路徑](../integration-services-paths.md)   
 [資料流程工作](../../control-flow/data-flow-task.md)  
  
  
