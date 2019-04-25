---
title: 進階模型 （資料採礦適用於 Excel 的增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bad97bf517bee9f8c2545d5a48acc02830dc5f58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637009"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>進階模型 (適用於 Excel 的資料採礦增益集)
  您可以使用**進階**資料模型化選項，以建立自訂資料採礦結構和模型使用參數所建立的精靈不同。 本章節描述的兩個精靈可幫助您建立全新的資料採礦結構，以及要套用到現有資料採礦結構的新採礦模型。  
  
## <a name="create-mining-structure"></a>建立採礦結構  
 ![建立採礦結構 按鈕，資料採礦功能區](media/dmc-createstruct.gif "Create Mining Structure] 按鈕，[資料採礦功能區")  
  
 **建立的採礦結構精靈**可協助您建立新的資料採礦結構。 結構就是擷取自指定之資料來源的資料集合。  採礦結構可以使用來源的新資料來更新，但是當您建立採礦結構時，就會定義資料類型和名稱，而這些資訊會定義資料用於分析的方式。  
  
 您可以使用下列資料來源來建立結構：Excel 資料表、Excel 範圍，或是外部資料來源中已經定義為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源檢視的任何資料。  
  
 對於每一個結構而言，您可以選擇將某些資料擱在一邊，以便將這些資料用於測試和驗證。 藉由建立這*鑑效組資料集*當您設定您的資料來源時，您可以確保所有以結構為基礎的模型，都能使用一致的資料集進行測試。  
  
 在建立採礦結構之後，您可以加入多個模型以套用不同的分析方法。  
  
 如需有關如何使用**建立採礦結構精靈**，請參閱[Create Mining Structure &#40;SQL Server 資料採礦增益集&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)。  
  
## <a name="add-model-to-structure"></a>將模型加入結構  
 ![將模型加入到結構按鈕](media/dmc-addmodel.gif "將模型加入結構 按鈕")  
  
 當您將新模型加入結構時，可使用不同演算法或不同參數來分析資料。 如果您想要使用資料採礦用戶端工具中未公開的其中一種演算法來建立模型，這個選項就特別有用。  
  
 例如，您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援的任何演算法，包括：  
  
-   線性迴歸  
  
-   時序群集  
  
-   巢狀資料集的關聯分析  
  
 若要查看有哪些種類的採礦結構，您可以瀏覽模型和結構儲存在[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]依序按一下 **管理模型**或是**瀏覽**。  
  
 但是，僅限於在目前工作階段期間建立的資料採礦結構，或是已儲存至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的採礦結構。  
  
 如需詳細資訊，請參閱 <<c0> [ 將模型加入結構&#40;適用於 Excel 的資料採礦增益集&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [管理模型&#40;SQL Server 資料採礦增益集&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [瀏覽模型，在 Excel 中的&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
