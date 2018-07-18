---
title: 設定字串存放區的維度和資料分割 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ae16d1e77e5e7dd16113bd8ee4ed4a0d5234668
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275704"
---
# <a name="configure-string-storage-for-dimensions-and-partitions"></a>設定維度及分割區的字串存放區
  您可以重新設定字串存放區，在超出字串存放區之 4 GB 檔案大小限制的維度屬性或分割區中容納非常大的字串。 如果您的維度或資料分割包含此大小的字串存放區，您可以在維度或資料分割層級，變更本機及連結 (本機或遠端) 物件的 **StringStoresCompatibilityLevel** 屬性來解決檔案大小限制。  
  
 請注意您可以只在需要額外容量的物件上加大字串存放區。 在大部分的維度模型中，字串資料會與維度相關聯。 但包分割區中最上層的字串若包含相異計數量值，也可以受益於此設定。 因為此設定係針對字串，所以數值資料不受影響。  
  
 這個屬性的有效值包括：  
  
|值|描述|  
|-----------|-----------------|  
|**1050**|指定每個存放區 4 GB 檔案大小上限的預設字串存放區架構。|  
|**1100**|指定較大的字串存放區，每個存放區最多支援 40 億個唯一字串。|  
  
> [!IMPORTANT]  
>  變更物件的字串存放區設定需要您重新處理物件本身以及任何相依物件。 完成此程序需要進行處理。  
  
 本主題包含下列幾節：  
  
-   [關於字串存放](#bkmk_background)  
  
-   [必要條件](#bkmk_prereq)  
  
-   [步驟 1：在 SQL Server Data Tools 中設定 StringStoreCompatiblityLevel 屬性](#bkmk_step1)  
  
-   [步驟 2：處理物件](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> 關於字串存放  
 字串存放區組態為選擇性，亦即，即使您建立新的資料庫，也會使用預設字串存放區架構 (檔案大小上限為 4 GB)。 使用較大的字串存放區架構對效能的影響雖然小但也顯著。 只有在您的字串存放區檔案接近或達到最大 4 GB 限制時，才使用它。  
  
> [!NOTE]  
>  這個設定不適用於資料採礦模型。 目前，包含資料採礦結構的模型仍然可能會有 GB 檔案大小限制。  
  
 在 Analysis Services 多維度資料庫中，字串與數值資料分開存放，以便根據資料的特性進行最佳化。 字串資料通常會在表示名稱或描述的維度屬性中找到。 字串資料也可以為在相異計數量值中。 字串資料也可以用於索引鍵。  
  
 您可以依字串存放的副檔名識別字串存放 (例如 asstore、.bstore、.ksstore 或 .string 檔)。 根據預設，這些檔案中的每一個都遵從最大 4 GB 的限制。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中，您可以指定允許字串存放區依需要成長的替代儲存機制，來覆寫檔案大小上限。  
  
 與限制實體檔案大小的預設字串存放區架構相比，較大的字串存放區是以字串數目上限為基礎。 較大的字串存放區的最大限制為 40 億個唯一字串，或 40 億筆記錄，以先發生者為準。 較大的字串存放區會針對偶數大小建立記錄，其中每筆記錄等於 64K 的頁面。 如果您有非常長，而且無法納入單一記錄的字串，則有效限制將少於 40 億個字串。  
  
##  <a name="bkmk_prereq"></a> 必要條件  
 您也必須有 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更新版的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 維度和分割區必須使用 MOLAP 儲存。  
  
 資料庫相容性層級必須設定為 1100。 如果您使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更新版的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]建立或部署資料庫，則資料庫相容性層級已經設定為 1100。 如果您將使用舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立的資料庫移到 ssSQL11 或更新版本，必須更新相容性層級。 如果是移動但未重新部署的資料庫，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 設定相容性層級。 如需詳細資訊，請參閱 <<c0> [ 設定多維度資料庫的相容性層級&#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)。</c0>  
  
##  <a name="bkmk_step1"></a> 步驟 1：在 SQL Server Data Tools 中設定 StringStoreCompatiblityLevel 屬性  
  
1.  使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]開啟包含您要修改之維度或資料分割的專案。  
  
2.  若要變更維度的字串存放區，請開啟 [方案總管]。 按兩下要修改其字串存放區的維度。  
  
3.  在 [維度設計師] 的 [屬性] 窗格中，確認已選取維度的父節點 (例如，如果維度是 Customers，選取 Customers 而不是其中一個子屬性)。  
  
4.  在 [屬性] 窗格的 [進階] 區段中，將 **StringStoresCompatibilityLevel** 設定為 **1100**。 針對需要較大儲存體的其他維度重複此作業，否則請將其餘維度保持在值 **1050** 。  
  
5.  針對分割區，從 [方案總管] 開啟 Cube。  
  
6.  按一下 [分割區] 索引標籤。  
  
7.  展開資料分割，選取需要額外儲存容量的資料分割，然後修改 **StringStoresCompatibilityLevel** 屬性。  
  
8.  儲存檔案。  
  
##  <a name="bkmk_step2"></a> 步驟 2：處理物件  
 處理物件之後，將會使用新的儲存體架構。 處理物件也會證明您已經成功解決儲存限制問題，因為先前回報字串存放溢位情況的錯誤應該不會再發生。  
  
-   在方案總管中，以滑鼠右鍵按一下您剛修改的維度，然後選取 [處理]。  
  
 您必須針對即將使用新字串存放架構的每個物件，使用 [完整處理] 選項。 在處理之前，請務必針對維度執行影響分析，以確認相依物件是否也需要處理。  
  
## <a name="see-also"></a>另請參閱  
 [工具和方式處理&#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [處理選項和設定&#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)   
 [資料分割儲存模式及處理](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)   
 [維度儲存](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)  
  
  
