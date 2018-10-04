---
title: Analysis Server 屬性對話方塊 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: afa6c20ccf591b4cea6917cd11817cb24c786abd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078058"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>Analysis Server 屬性對話方塊 (Analysis Services)
  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [Analysis Server 屬性] 對話方塊，即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的一般、語言/定序和安全性設定。 以滑鼠右鍵按一下**物件總管**中的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體，然後從操作功能表選取 [屬性]，即可顯示 [Analysis Server 屬性] 對話方塊。 **[Analysis Server 屬性]** 對話方塊包含以下屬性。  
  
## <a name="information-properties"></a>資訊屬性  
 使用此頁面來檢視伺服器模式、版本和相容性層級。 每個執行個體都會以表格式或多維度伺服器模式安裝，能夠載入表格式或多維度模型。 如果您必須支援這兩個模式，則必須安裝兩個執行個體。  
  
 **支援的相容性層級**相當於`DefaultCompatibilityLevel`AMO 中的屬性。 根據安裝期間所指定的伺服器部署模式，它是唯讀的。 伺服器在執行因伺服器模式或版本而異的作業 (例如將表格式資料庫的備份還原到表格式伺服器執行個體中) 時，會檢查這個屬性。 請勿將它與表格式或多維度模型的資料庫相容性模式搞混 (後者有類似的名稱和值)。 這個伺服器屬性的有效值包括：  
  
-   **1100** 是部署模式 0 (適用於多維度和資料採礦模式) 的預設相容性層級。  
  
-   **1103** 是部署模式 1 或 2 (適用於支援表格式模式或 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]的安裝) 的預設相容性層級。  
  
 當支援命名空間的用戶端要求 DISCOVER_XML_METADATA 時，伺服器會傳回這個值。 如需詳細資訊，請參閱 [DISCOVER_XML_METADATA 資料列集](schema-rowsets/xml/discover-xml-metadata-rowset.md)。  
  
## <a name="general-properties"></a>一般屬性  
 使用此頁面即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的基本和進階一般屬性，例如資料夾位置和網路設定。  
  
 伺服器屬性頁面只會顯示管理員很有可能變更的屬性，例如用來針對某些設定微調伺服器的記憶體和執行緒集區屬性。 下列清單提供主要屬性群組的連結：  
  
-   [一般屬性](server-properties/general-properties.md)  
  
-   [資料採礦屬性](server-properties/data-mining-properties.md)  
  
-   [功能屬性](server-properties/feature-properties.md)  
  
-   [檔案存放區屬性](server-properties/filestore-properties.md)  
  
-   [鎖定管理員屬性](server-properties/lock-manager-properties.md)  
  
-   [記錄屬性](server-properties/log-properties.md)  
  
-   [記憶體屬性](server-properties/memory-properties.md)  
  
-   [網路屬性](server-properties/network-properties.md)  
  
-   [OLAP 屬性](server-properties/olap-properties.md)  
  
-   [安全性屬性](server-properties/security-properties.md)  
  
-   [執行緒集區屬性](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>語言/定序屬性  
 使用此頁面即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的預設語言和定序選項。 下列清單包含每個選項的簡短描述。 如需更詳細的描述，請參閱[語言和定序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)。  
  
-   **[二進位]** 是用來根據為每個字元定義的位元模式排序和比較資料。 二進位排序順序有區分大小寫，亦即小寫優先於大寫，而且有區分腔調字。 這是最快的排序順序。  
  
     如果沒有選取此選項， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會遵循相關聯之語言或字母字典中所定義的排序和比較規則。  
  
    > [!NOTE]  
    >  如果選取此選項，會停用 [區分大小寫]、[區分腔調字]、[區分假名] 和 [區分全半形] 等選項。  
  
-   **[二進位 2]** 是用來根據為每個字元定義的位元模式排序和比較 Unicode 資料。 二進位排序順序有區分大小寫，亦即小寫優先於大寫，而且有區分腔調字。 這是最快的排序順序。  
  
-   [區分大小寫] 是用來根據針對關聯之語言或字母提供的字典規則來排序和比較資料，以及區別大寫和小寫字母。  
  
     如果未選取此選項， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將大小寫字母視為相同。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 未定義小寫字母排序較低或更高的版本比大寫子母**區分大小寫**未選取。  
  
-   [區分腔調字] 是用來根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別有腔調和無腔調字元。 例如，'a' 不等於 'á'。  
  
     如果未選取此選項， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將有腔調與無腔調的字母視為相同。  
  
-   [區分假名] 是用來根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別兩種日文假名字元：平假名和片假名。  
  
     如果未選取此選項， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將平假名與片假名字元視為相同。  
  
-   [區分全半形] 是用來根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別單一位元組字元 (半形) 和使用雙位元組字元 (全形) 表示的相同字元。  
  
     如果未選取此選項，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將相同字元的單一位元組與雙位元組表示方式視為相同。  
  
## <a name="security-properties"></a>安全性屬性  
 使用此頁面即可指定屬於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器管理員角色的 Windows 使用者與群組帳戶。 此角色的成員資格會傳達執行伺服器範圍之工作的權限，例如建立或處理資料庫、修改伺服器屬性、新增或移除這個角色的其他成員或是啟動追蹤。 請參閱[授與伺服器系統管理員權限&#40;Analysis Services&#41; ](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)如需詳細資訊。  
  
## <a name="see-also"></a>另請參閱  
 [判斷 Analysis Services 執行個體的伺服器模式](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Analysis Services 中設定伺服器屬性](server-properties/server-properties-in-analysis-services.md)   
 [支援的 Analysis Services 的驗證方法](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [角色和權限&#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [語言和定序&#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
