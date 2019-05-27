---
title: 定義維度的排序方式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05e75eb726d67e992a0a9320be8d23bbc547bedb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076854"
---
# <a name="define-the-ordering-for-a-dimension"></a>定義維度的排序方式
  將屬性排序方式增強功能加入至 Cube 或維度，即可指定如何排序屬性的成員。 您可以依名稱或屬性的索引鍵來排序成員，或是依名稱或另一個屬性 (根據屬性關聯性) 的索引鍵來排序成員。 依預設，會依名稱來排序成員。 這項增強功能會在維度中變更屬性的 `OrderBy` 和 `OrderByAttributeID` 屬性設定。  
  
 若要加入屬性排序，您可使用 [商業智慧精靈]，並於 [選擇增強功能] 頁面上選取 [指定屬性排列方式] 選項。 然後，此精靈會引導您逐步完成選取要套用屬性排序方式的維度，並指定如何為選取的維度排序屬性。  
  
## <a name="selecting-a-dimension"></a>選取維度  
 在精靈的第一個 [指定屬性排列方式] 頁面上，您指定要套用屬性排列方式的維度。 加入到此選取維度的屬性排列方式增強功能，會造成維度的變更。 包含選取之維度的所有 Cube，都會繼承這些變更。  
  
## <a name="specifying-ordering"></a>指定排列方式  
 在精靈的第二個 [指定屬性排列方式] 頁面上，您指定如何排序維度中的所有屬性。  
  
 在 [排序屬性] 資料行中，您可變更用於執行排序的屬性。 如果您想要用來排序成員的屬性不在清單中，向下捲動清單，然後按 **\<新增屬性...> >** 以開啟**選取資料行**對話方塊中，您可以在其中選取維度資料表中的資料行。 使用 [選取資料行] 對話方塊選取資料行會建立一個額外的屬性，可用它來排序屬性的成員。  
  
 在 [準則] 資料行中，您可選取要依 [索引鍵] 或 [名稱] 來排序屬性的成員。  
  
  
