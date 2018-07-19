---
title: 使用彙總轉換來彙總資料集中的值 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e48ad3870ce3381851fd454d76661f168ea1c1fc
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404430"
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>使用彙總轉換來彙總資料集中的值
  若要加入及設定「彙總」轉換，封裝中必須已包含至少一個「資料流程」工作和一個來源。  
  
### <a name="to-aggregate-values-in-a-dataset"></a>若要彙總資料集中的值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後從 **[工具箱]** 拖曳「彙總」轉換至設計介面。  
  
4.  從來源或先前的轉換將連接子拖曳到彙總轉換，以便將彙總轉換連接到資料流程。  
  
5.  按兩下該轉換。  
  
6.  在 **[彙總轉換編輯器]** 對話方塊中，按一下 **[彙總]** 索引標籤。  
  
7.  在 **[可用的輸入資料行]** 清單中，選取您要計算彙總值之資料行旁邊的核取方塊。 選取的資料行便會顯示在資料表中。  
  
    > [!NOTE]  
    >  您可以多次選取某個資料行，以套用多個轉換至該資料行。 為了唯一識別彙總，會在資料行輸出別名的預設名稱後面附加一個數字。  
  
8.  (選擇性) 修改 **[輸出別名]** 資料行中的值。  
  
9. 若要變更預設彙總作業 **[群組依據]**，請在 **[作業]** 清單中選取不同的作業。  
  
10. 若要變更預設比較，請選取 **[比較旗標]** 資料行中列出的個別比較旗標。 依預設，比較會忽略大小寫、假名類型、不佔空間字元和字元寬度。  
  
11. (選擇性) 針對 **[計算相異]** 彙總，在 **[計算相異索引鍵]** 資料行中指定相異值的確實數目，或是在 **[計算相異小數位數]** 資料行中選取近似計數。  
  
    > [!NOTE]  
    >  提供相異值的數目 (不論是精確值或近似值) 可最佳化效能，因為轉換可以預先配置適當的記憶體容量來執行其工作。  
  
12. (選擇性) 按一下 **[進階]** ，並更新「彙總」轉換輸出的名稱。 如果彙總包含 **Group By** 作業，您可以在 **[索引鍵小數位數]** 資料行中，選取群組索引鍵值的近似計數，或是在 **[索引鍵]** 資料行中，指定群組索引鍵值的確實數目。  
  
    > [!NOTE]  
    >  提供相異值的數目 (不論是精確值或近似值) 可最佳化效能，因為轉換可以預先配置適當的記憶體容量來執行其工作。  
  
    > [!NOTE]  
    >  **[索引鍵小數位數]** 和 **[索引鍵]** 選項互斥。 如果您同時在兩個資料行中輸入值，將會使用 **[索引鍵小數位數]** 或 **[索引鍵]** 中較大的值。  
  
13. (選擇性) 按一下 **[進階]** 索引標籤，並設定可以用來最佳化彙總轉換執行之所有作業的屬性。  
  
14. 按一下 [確定] 。  
  
15. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [彙總轉換](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../../integration-services/data-flow/integration-services-paths.md)   
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)  
  
  
