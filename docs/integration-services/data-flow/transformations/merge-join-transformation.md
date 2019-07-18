---
title: 合併聯結轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergejointrans.f1
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 785f7f0af9a41052a870edc8feaf566585a45e89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725975"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  合併聯結轉換提供藉由使用 FULL、LEFT 或 INNER 聯結，來聯結兩個已排序資料集所產生的輸出。 例如，您可以使用 LEFT 聯結來聯結包含產品資訊的資料表，以及列出製造產品的國家/地區的資料表。 此結果為列出所有產品及其原產國家/地區的資料表。  
  
 您可以利用下列方式設定「合併聯結」轉換：  
  
-   指定聯結為 FULL、LEFT 或 INNER 聯結。  
  
-   指定聯結使用的資料行。  
  
-   指定轉換是否要將 Null 值當作相當於其他 Null 處理。  
  
    > [!NOTE]  
    >  如果 Null 值未當成相等值，則轉換會以與 SQL Server Database Engine 相同的方式處理 Null 值。  
  
 這個轉換有兩個輸入與一個輸出。 它不支援錯誤輸出。  
  
## <a name="input-requirements"></a>輸入需求  
 合併聯結轉換針對其輸入需要已排序的資料。 如需這項重要需求的詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
## <a name="join-requirements"></a>聯結需求  
 合併聯結轉換會要求聯結的資料行擁有相符的中繼資料。 例如，您無法聯結數值資料類型的資料行，與字元資料類型的資料行。 如果資料是字串資料類型，第二個輸入中的資料行長度就必須小於或等於與其合併之第一個輸入中的資料行長度。  
  
## <a name="buffer-throttling"></a>緩衝區調整  
 您再也不必設定 **MaxBuffersPerInput** 屬性的值，因為 Microsoft 已做出變更，降低合併聯結轉換會耗用過多記憶體的風險。 這個問題有時候會發生在合併聯結的多個輸入以不平均的速率產生資料時。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關如何設定此轉換屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用合併聯結轉換來擴充資料集](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-join-transformation-editor"></a>合併聯結轉換編輯器
  使用 [合併聯結轉換編輯器]  對話方塊，即可指定合併兩個由聯結組合之輸入的聯結類型、聯結資料行以及輸出資料行。  
  
> [!IMPORTANT]  
>  合併聯結轉換針對其輸入需要已排序的資料。 如需這項重要需求的詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
### <a name="options"></a>選項。  
 **聯結類型**  
 指定要使用內部聯結、左方外部聯結或完整聯結。  
  
 **交換輸入**  
 使用 [交換輸入]  按鈕，來切換輸入之間的順序。 此選取項目對於左方外部聯結選項可能非常有用。  
  
 **輸入**  
 針對您要放入合併輸出中的每個資料行，首先從可用的輸入清單中選取。  
  
 輸入會以兩個個別的資料表來顯示。 選取要包含在輸出中的資料行。 拖曳資料行以建立資料表之間的聯結。 若要刪除聯結，請選取聯結然後按下 DELETE 鍵。  
  
 **輸入資料行**  
 從所選輸入上之可用的資料行清單中，選取要包含在合併輸出中的資料行。  
  
 **輸出別名**  
 輸入每一個輸出資料行的別名。 預設是輸入資料行的名稱；但是，您可以選擇任何唯一的、描述性名稱。  
  
## <a name="see-also"></a>另請參閱  
 [合併轉換](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [聯集全部轉換](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
