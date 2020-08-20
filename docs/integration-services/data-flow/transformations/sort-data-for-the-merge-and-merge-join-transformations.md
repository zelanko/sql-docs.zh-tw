---
description: 排序合併和合併聯結轉換的資料
title: 排序合併和合併聯結轉換的資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- sort attributes [Integration Services]
- output columns [Integration Services]
ms.assetid: 22ce3f5d-8a88-4423-92c2-60a8f82cd4fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5a9d622868c934065a47b6bb3c02b49b4de36371
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495691"
---
# <a name="sort-data-for-the-merge-and-merge-join-transformations"></a>排序合併和合併聯結轉換的資料

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]中，「合併」和「合併聯結」轉換需要針對其輸入排序的資料。 輸入資料必須實際排序，且必須在來源中或上游轉換中設定輸出和輸出資料行的排序選項。 如果排序選項表示資料已排序，但實際上資料並未排序，則合併或合併聯結作業的結果可能無法預測。  
  
## <a name="sorting-the-data"></a>排序資料  
 您可以使用下列其中一個方法來排序此資料：  
  
-   在來源的陳述式中，使用載入資料所使用的 ORDER BY 子句。  
  
-   在資料流程中，將「排序」轉換插入到「合併」或「合併聯結」轉換之前。  
  
 如果資料是字串資料，「合併」和「合併聯結」轉換都會預期這些字串值已經使用 Windows 定序排序了。 若要提供字串值給使用 Windows 定序排序的「合併」和「合併聯結」轉換，請使用下列程序。  
  
#### <a name="to-provide-string-values-that-are-sorted-by-using-windows-collation"></a>若要提供使用 Windows 定序排序的字串值  
  
-   使用「排序」轉換來排序資料。  
  
     「排序」轉換會使用 Windows 定序來排序字串值。  
  
     -或-  
  
-   使用 Transact-SQL CAST 運算子，先將 **varchar** 值轉換成 **nvarchar** 值，再使用 Transact-SQL ORDER BY 子句來排序資料。  
  
    > [!IMPORTANT]  
    >  您無法單獨使用 ORDER BY 子句，因為 ORDER BY 子句會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 定序來排序字串值。 如果您使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 定序，可能會產生與 Windows 定序不同的排序次序，進而導致「合併」或「合併聯結」轉換產生非預期的結果。  
  
## <a name="setting-sort-options-on-the-data"></a>設定資料的排序選項  
 有兩個重要的排序屬性必須針對將資料提供給「合併」和「合併聯結」轉換的來源或上游轉換設定：  
  
-   輸出的 **IsSorted** 屬性，表示資料是否經過排序。 此屬性必須設定為 **True**。  
  
    > [!IMPORTANT]  
    >  將 **IsSorted** 屬性的值設定為 **True** 時，不會排序資料。 此屬性僅針對資料先前已經過排序的下游元件提供提示。  
  
-   輸出資料行的 **SortKeyPosition** 屬性，指出資料行是否經過排序、資料行的排序次序，以及排序多個資料行的順序。 此屬性必須針對已排序資料的每個資料行設定。  
  
 如果您使用「排序」轉換排序資料，「排序」轉換會同時設定「合併」或「合併聯結」轉換所需的屬性。 也就是說，「排序」轉換會將其輸出的 **IsSorted** 屬性設定為 **True**，並設定其輸出資料行的 **SortKeyPosition** 屬性。  
  
 不過，如果您沒有使用「排序」轉換排序資料，則必須在來源或上游轉換手動設定這些排序屬性。 若要在來源或上游轉換手動設定排序屬性，請使用下列程序。  
  
#### <a name="to-manually-set-sort-attributes-on-a-source-or-transformation-component"></a>若要手動在來源或轉換元件上設定排序屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 **[資料流程]** 索引標籤上，找出適當的來源或上游轉換，或者將其從 **[工具箱]** 拖曳到設計介面。  
  
4.  以滑鼠右鍵按一下元件，然後按一下 [顯示進階編輯器]  。  
  
5.  按一下 **[輸入與輸出屬性]** 索引標籤。  
  
6.  按一下 [\<component name> 輸出]，然後將 **IsSorted** 屬性設定為 **True**。  
  
    > [!NOTE]  
    >  如果您手動將輸出的 **IsSorted** 屬性設定為 **True** 而且資料未排序，則當您執行封裝時，下游「合併」或「合併聯結」轉換中可能會有資料遺失或是不正確的資料比較。  
  
7.  展開 **[輸出資料行]** 。  
  
8.  按一下要表示為已排序的資料行，並按照下列指導方針，將其 **SortKeyPosition** 屬性設定為非零整數值：  
  
    -   整數值必須表示數值順序，且從 1 開始並以 1 為遞增值。  
  
    -   正整數值表示遞增排序次序。  
  
    -   負整數值表示遞減排序次序 (如果設定為負數，數字的絕對值會決定資料行在排序順序中的位置)。  
  
    -   預設值 0 表示未排序資料行。 針對不參與排序的輸出資料行，將其值保留為 0。  
  
     關於如何設定 **SortKeyPosition** 屬性的範例，請考慮使用載入來源資料的下列 Transact-SQL 陳述式：  
  
     `SELECT * FROM MyTable ORDER BY ColumnA, ColumnB DESC, ColumnC`  
  
     針對此陳述式，設定每個資料行的 **SortKeyPosition** 屬性，如下所示：  
  
    -   將 ColumnA 的 **SortKeyPosition** 屬性設定為 1。 這表示 ColumnA 是要排序的第一個資料行，而且是以遞增順序排序。  
  
    -   將 ColumnB 的 **SortKeyPosition** 屬性設定為 -2。 這表示 ColumnB 是要排序的第二個資料行，而且是以遞減順序排序  
  
    -   將 ColumnC 的 **SortKeyPosition** 屬性設定為 3。 這表示 ColumnC 是要排序的第三個資料行，而且是以遞增順序排序。  
  
9. 針對每個已排序的資料行重複步驟 8。  
  
10. 按一下 [確定]  。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [合併轉換](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [合併聯結轉換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../../integration-services/data-flow/integration-services-paths.md)   
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)  
  
  
