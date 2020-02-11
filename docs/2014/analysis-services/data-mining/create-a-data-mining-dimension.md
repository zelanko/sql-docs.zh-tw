---
title: 建立資料採礦維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], dimensions
ms.assetid: 9f0c39e5-3516-43ab-b203-f3f6dbcff89a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b642d7a0bdf552d8944602761aa76eec1cf35306
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085495"
---
# <a name="create-a-data-mining-dimension"></a>建立資料採礦維度
  如果採礦結構是以 OLAP Cube 為基礎，您就可以建立一個包含採礦模型內容的維度。 然後您就可以將維度併入來源 Cube 中。  
  
 您也可以瀏覽維度、用它來瀏覽模型結果，或是使用 MDX 查詢維度。  
  
### <a name="to-create-a-data-mining-dimension"></a>若要建立資料採礦維度  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的資料採礦設計師中，選取 [採礦結構]**** 索引標籤或 [採礦模型]**** 索引標籤。  
  
2.  從 [採礦模型]**** 功能表，選取 [建立資料採礦維度]****。  
  
     [建立資料採礦維度]**** 對話方塊隨即開啟。  
  
3.  在 [建立資料採礦維度]**** 對話方塊的 [模型名稱]**** 清單中，選取 OLAP 採礦模型。  
  
4.  在 [維度名稱]**** 方塊中，輸入新資料採礦維度的名稱。  
  
5.  如果您想要建立包含新資料採礦維度的 Cube，請選取 [建立 Cube]****。 在選取 [建立 Cube]**** 之後，您就可以輸入 Cube 的新名稱。  
  
6.  按一下 [確定]  。  
  
     這時會建立資料採礦維度，並加入方案總管的 [維度]**** 資料夾。 如果您選取 [建立 Cube]****，則也會建立新的 Cube，並將其加入 [Cubes]**** 資料夾。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和使用說明](mining-structure-tasks-and-how-tos.md)  
  
  
