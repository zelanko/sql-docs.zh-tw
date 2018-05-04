---
title: 建立資料採礦維度 |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f6e22cca047b5d196268d8d291db372ba07af0a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-data-mining-dimension"></a>建立資料採礦維度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果採礦結構是以 OLAP Cube 為基礎，您就可以建立一個包含採礦模型內容的維度。 然後您就可以將維度併入來源 Cube 中。  
  
 您也可以瀏覽維度、用它來瀏覽模型結果，或是使用 MDX 查詢維度。  
  
### <a name="to-create-a-data-mining-dimension"></a>若要建立資料採礦維度  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的資料採礦設計師中，選取 [採礦結構] 索引標籤或 [採礦模型] 索引標籤。  
  
2.  從 [採礦模型] 功能表，選取 [建立資料採礦維度]。  
  
     [建立資料採礦維度] 對話方塊隨即開啟。  
  
3.  在 [建立資料採礦維度] 對話方塊的 [模型名稱] 清單中，選取 OLAP 採礦模型。  
  
4.  在 [維度名稱] 方塊中，輸入新資料採礦維度的名稱。  
  
5.  如果您想要建立包含新資料採礦維度的 Cube，請選取 [建立 Cube]。 在選取 [建立 Cube] 之後，您就可以輸入 Cube 的新名稱。  
  
6.  按一下 **[確定]**。  
  
     這時會建立資料採礦維度，並加入方案總管的 [維度] 資料夾。 如果您選取 [建立 Cube]，則也會建立新的 Cube，並將其加入 [Cubes] 資料夾。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和使用說明](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
