---
title: 預覽選取的資料表 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.previewselecttable.f1
ms.assetid: b6b34b5a-43b3-4a75-9f3b-b2ad1084b1b6
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49207b2d1574593c14ca6b005febebb28864dec3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314984"
---
# <a name="preview-selected-table-ssas"></a>預覽選取的資料表 (SSAS)
  **[資料表匯入精靈]** 的這個頁面可讓您預覽選定資料表中的資料、選取要併入資料匯入的資料行，以及在選取的資料行中篩選資料。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 並非資料表中的所有資料列都會顯示。 但是，您設定的篩選將會在匯入期間套用至資料表中的所有資料。  
  
 針對使用 Windows 驗證的資料來源，目前使用者的認證會用來提取顯示在 [預覽和篩選] 對話方塊中的資料。 至於其他資料來源，連接字串中提供的認證則用來提取資料。  
  
 此頁面之資料的外觀不保證匯入將會成功。 如果在 [模擬資訊] 頁面中指定的使用者名稱未具備從所選資料庫讀取的權限，則匯入將會失敗。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **資料行標頭中的核取方塊**  
 選取核取方塊可將資料行納入資料匯入作業。 清除核取方塊可從資料匯入作業排除資料行。  
  
 **資料行標頭中的向下箭頭按鈕**  
 篩選資料行中的資料。  
  
 **清除資料列篩選**  
 移除已經套用到資料行中資料的所有篩選。  
  
  
