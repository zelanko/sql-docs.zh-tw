---
title: 一般（資料庫設計工具）（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bf87f2441488810286523a75137a3285aabc1956
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081076"
---
# <a name="general-database-designer-analysis-services---multidimensional-data"></a>一般 (資料庫設計工具) (Analysis Services - 多維度資料)
  使用 **[一般]** 索引標籤，即可變更 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的屬性。  
  
 **顯示一般索引標籤**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案。  
  
2.  在方案總管**** 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案，再按一下 [編輯資料庫]****，然後按一下 [一般]**** 索引標籤。  
  
## <a name="basic-options"></a>基本選項  
 展開 **[基本]** 區段來修改資料庫的基本資訊。 此區段包含下列選項：  
  
 **資料庫名稱**  
 顯示資料庫的名稱。  
  
> [!NOTE]  
>  若要重新命名資料庫，請在方案總管**** 視窗中以滑鼠右鍵按一下專案，然後按一下 [屬性]****。 在資料庫的 **[屬性頁]** 對話方塊中，於 **[部署]** 頁面上，將 **[資料庫]** 屬性的值變更為新的資料庫名稱。  
  
 **描述**  
 鍵入資料庫的描述。  
  
## <a name="translations-options"></a>翻譯選項  
 展開 **[翻譯]** 區段，即可建立和修改資料庫標題和描述的翻譯。 此區段包含具有下列資料行的方格：  
  
 **語言**  
 選取指定交易的語言。  
  
 若要將新翻譯加入方格中，請按一下** \<[加入新翻譯]>**。  
  
 **翻譯的標題**  
 以適當的翻譯語言鍵入資料庫的標題。 如果空白，則會使用資料庫的預設標題。  
  
 **已翻譯描述**  
 以適當的翻譯語言鍵入資料庫的描述。 如果空白，則會使用資料庫的預設描述。  
  
## <a name="account-type-mapping-options"></a>帳戶類型對應選項  
 展開 **[帳戶類型對應]** 區段，以修改所選取資料庫中，與每一個帳戶 **類型** 相關聯的預設彙總函式。  
  
> [!NOTE]  
>   此選項僅適用於有一個或多個量值使用 *ByAccount* 彙總函式的 Cube。  
  
 此區段包含具有下列資料行的方格：  
  
 **名稱**  
 鍵入帳戶類型的名稱。  
  
 若要加入新的帳戶類型，請按一下** \<[新增帳戶類型>**]。  
  
 **鋸齒**  
 設定供商業智慧精靈使用之帳戶類型的預設名稱。 如果此資料行保留空白，則會使用 **[名稱]** 資料行中的預設值。  
  
 **彙總函式**  
 選取用於所選取帳戶類型的彙總函式。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型資料庫 &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)   
 [警告 &#40;資料庫設計工具&#41; &#40;Analysis Services-多維度資料&#41;](warnings-database-designer-analysis-services-multidimensional-data.md)  
  
  
