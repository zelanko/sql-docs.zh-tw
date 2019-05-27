---
title: 模糊查閱轉換編輯器 （參考資料表索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c9fb11308ae60cf061f184ade467d814d6a10fc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058310"
---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>模糊查閱轉換編輯器 (參考資料表索引標籤)
  使用 **[模糊查閱轉換編輯器]** 對話方塊的 **[參考資料表]** 索引標籤，指定來源資料表和用於查閱的索引。 參考資料來源必須是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中的資料表。  
  
> [!NOTE]  
>  模糊查閱轉換會建立參考資料表的工作副本。 下面描述的索引是使用特殊資料表，而非使用一般 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 索引在此工作資料表上建立的。 除非您選取 **[維護儲存的索引]**，否則轉換不會修改現有的來源資料表。 在此情況下，它會在參考資料表上建立觸發程序，以根據參考資料表的變更來更新工作資料表和查閱索引資料表。  
  
> [!NOTE]  
>  `Exhaustive`而`MaxMemoryUsage`模糊查閱 」 轉換的屬性不適用於**模糊查閱轉換編輯器**，但可以透過設定**進階編輯器**。 此外，大於 100 的值`MaxOutputMatchesPerInput`您可以只在指定**進階編輯器**。 如需有關這些屬性的詳細資訊，請參閱＜ [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)＞的「模糊查閱轉換」一節。  
  
 若要深入了解模糊查閱轉換，請參閱＜ [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md)＞。  
  
## <a name="options"></a>選項  
 **[無快取]**  
 從清單中選取現有的 OLE DB 連線管理員，或按一下 [新增] 來建立新連線。  
  
 **新增**  
 使用 [設定 OLE DB 連接管理員] 對話方塊來建立新的連接。  
  
 **產生新的索引**  
 指定轉換應建立新的索引以用來查閱。  
  
 **參考資料表名稱**  
 選取要用來作為參考 (查閱) 資料表的現有資料表。  
  
 **儲存新的索引**  
 如果您要儲存新的查閱索引，請選取此選項。  
  
 **新增索引名稱**  
 如果您已選擇要儲存新的查閱索引，請輸入該索引的描述性名稱。  
  
 **[維護儲存的索引]**  
 如果您已選擇要儲存新的查閱索引，請指定是否也要 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 維護該索引。  
  
> [!NOTE]  
>  當您在 **[模糊查閱轉換編輯器]** 的 **[參考資料表]** 索引標籤上選取 **[維護儲存的索引]** 時，轉換會使用具名預存程序來維護索引。 這些 Managed 預存程序會使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的 Common Language Runtime (CLR) 整合功能。 根據預設，不會啟用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 CLR 整合功能。 若要使用 **[維護儲存的索引]** 功能，您必須啟用 CLR 整合。 如需詳細資訊，請參閱 [Enabling CLR Integration](../relational-databases/clr-integration/clr-integration-enabling.md)。  
>   
>  因為 **[維護儲存的索引]** 選項需要 CLR 整合，因此只有當您在已啟用 CLR 整合的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上選取參考資料表時，這項功能才有效。  
  
 **使用現有的索引**  
 指定轉換應使用現有的索引來查閱。  
  
 **現有索引的名稱**  
 從清單中選取先前建立的查閱索引。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [模糊查閱轉換編輯器 &#40;資料行索引標籤&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [模糊查閱轉換編輯器 &#40;進階索引標籤&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
