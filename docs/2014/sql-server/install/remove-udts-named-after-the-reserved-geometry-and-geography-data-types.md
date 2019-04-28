---
title: 移除保留的 GEOMETRY 和 GEOGRAPHY 資料類型命名的 UDTs |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f93b179da229793c65db452e4f38bb1f08fbfad1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855881"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>移除依據保留之 GEOMETRY 和 GEOGRAPHY 資料類型所命名的 UDT
  Upgrade Advisor 偵測到依據針對 `geometry` 或 `geography` 資料類型保留之詞彙所命名的使用者定義型別 (UDT)。 `geometry` 和 `geography` 資料類型屬於空間資料功能的一部分。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 用於空間資料類型的詞彙不應該當做 Common Language Runtime (CLR) 或別名 UDT 的名稱使用。  
  
## <a name="corrective-action"></a>更正動作  
 請移除依據此資料類型所命名的 UDT，然後使用未保留的名稱重新建立 UDT。  
  
## <a name="external-resources"></a>外部資源  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
