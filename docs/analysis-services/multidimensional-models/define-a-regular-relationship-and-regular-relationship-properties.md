---
title: 定義一般關聯性及一般關聯性屬性 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ee79742f919d7f47ae73968666d96622e3429bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209022"
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>定義一般關聯性及一般關聯性屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您定義新的 Cube 維度或新的量值群組時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試偵測是否有一般關聯性，然後將維度使用方式設定設為 [一般]  。 在 Cube 設計師的 [維度使用方式]  索引標籤上，您可以檢視或編輯一般維度關聯性。  
  
 當您定義 Cube 維度與量值群組的關聯性時，會同時為該關聯性指定資料粒度屬性。 資料粒度屬性會針對該維度定義 Cube 中可用之詳細資料的最低層級，這通常是維度的索引鍵屬性。 然而，有時您可能會想要在特定量值群組中，將特定 Cube 維度的資料粒度設定為不同的資料粒度。 例如，如果您使用的是 [銷售配額] 或 [預算] 量值群組，則可能會想要將 [時間] 維度的資料粒度屬性設定為 [月] 屬性而不是 [日] 屬性。 當您將資料粒度屬性指定為索引鍵屬性以外的屬性時，則必須確定維度中的其他所有屬性都是透過屬性關聯性直接或間接連結至另一個屬性。 否則， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將無法正確地彙總資料。  
  
  
