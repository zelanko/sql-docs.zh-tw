---
title: 定義一般關聯性及一般關聯性屬性 |Microsoft Docs
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
- granularity attribute
- relationships [Analysis Services], regular relationships
ms.assetid: 840280d8-20c3-46c0-99ea-62479469c36b
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dbf4b0f179c0c4ba0990b8fe61b2cd2a7584f058
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211928"
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>定義一般關聯性及一般關聯性屬性
  當您定義新的 Cube 維度或新的量值群組時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試偵測是否有一般關聯性，然後將維度使用方式設定設為 `Regular`。 在 Cube 設計師的 [維度使用方式] 索引標籤上，您可以檢視或編輯一般維度關聯性。  
  
 當您定義 Cube 維度與量值群組的關聯性時，會同時為該關聯性指定資料粒度屬性。 資料粒度屬性會針對該維度定義 Cube 中可用之詳細資料的最低層級，這通常是維度的索引鍵屬性。 然而，有時您可能會想要在特定量值群組中，將特定 Cube 維度的資料粒度設定為不同的資料粒度。 例如，如果您使用的是 [銷售配額] 或 [預算] 量值群組，則可能會想要將 [時間] 維度的資料粒度屬性設定為 [月] 屬性而不是 [日] 屬性。 當您將資料粒度屬性指定為索引鍵屬性以外的屬性時，則必須確定維度中的其他所有屬性都是透過屬性關聯性直接或間接連結至另一個屬性。 否則， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將無法正確地彙總資料。  
  
  
