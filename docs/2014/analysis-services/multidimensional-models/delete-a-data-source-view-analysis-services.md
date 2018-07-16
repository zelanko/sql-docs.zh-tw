---
title: 刪除資料來源檢視 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting data source views
- data source views [Analysis Services], deleting
- removing data source views
ms.assetid: ae3f5ca0-ecbf-4b52-8386-eb457719d854
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c8d04731a4b555b6e4afe9c8697fc5c4f907a9a1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284016"
---
# <a name="delete-a-data-source-view-analysis-services"></a>刪除資料來源檢視 (Analysis Services)
  如果您不再需要使用 OLAP 專案中的某個資料來源檢視 (DSV)，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 從專案中刪除檢視。  
  
 刪除 DSV 是一個永久動作。 您無法將已刪除的 DSV 還原到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫。  
  
 您無法從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以線上模式開啟的 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 資料庫中，刪除其他物件所相依的 DSV。 若要從連接到伺服器上執行之資料庫的專案中刪除 DSV，您必須先從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中刪除相依於該 DSV 的所有物件，再刪除 DSV 本身。  
  
 刪除 DSV 會使其他相依的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件無效，因此在您刪除 DSV 之前，請查看移除 DSV 後會變成無效的物件清單。 請仔細檢閱此清單，以確保清單中未包含您仍要使用的物件。  
  
 ![刪除物件 對話方塊](../media/ssas-olapdsv-deleteobjects.gif "刪除物件 對話方塊")  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](data-source-views-in-multidimensional-models.md)   
 [變更資料來源檢視中的屬性&#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md)  
  
  
