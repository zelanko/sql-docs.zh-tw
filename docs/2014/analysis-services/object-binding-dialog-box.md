---
title: 物件繫結 對話方塊 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.objectbinding.f1
helpviewer_keywords:
- Object Binding dialog box
ms.assetid: 2bb5ad7c-2962-4559-8c95-cf7148bd2e72
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 13b0050733b21e99ac7395a26953338f4dbce176
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033967"
---
# <a name="object-binding-dialog-box"></a>物件繫結對話方塊
  使用 **中的** [物件繫結] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 對話方塊，即可定義 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件屬性與資料來源檢視中之資料表或資料行之間的繫結。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [屬性] 視窗中，從下列 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件屬性值的下拉式清單中選取 [(新增)]，即可顯示 [物件繫結] 對話方塊：  
  
-   NameColumn  
  
-   ValueColumn  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   UnaryOperatorColumn  
  
## <a name="options"></a>選項。  
 **繫結型別**  
 選取要用於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件的繫結。 可以使用下列類型的繫結：  
  
 資料行繫結  
 將物件繫結到資料來源檢視中的現有資料表和資料行。  
  
 產生資料行  
 指出要在資料來源檢視中定義新的資料行，然後建立資料行繫結與該資料行的關聯。  
  
> [!NOTE]  
>  如果選取此選項，您就必須在部署 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件之前，先執行 [結構描述產生精靈]。  
  
 資料列繫結  
 將物件繫結到事實資料表中的資料列，並可根據事實資料表中處理的資料列數提供計數量值。  
  
 **來源資料表**  
 顯示與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件相關聯之資料來源檢視中的資料表清單。  
  
 **來源資料行**  
 顯示 [來源資料表] 中選取之資料表內的資料行清單。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  