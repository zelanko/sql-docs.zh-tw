---
title: 快速剖析 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- fast parse [Integration Services]
ms.assetid: 6688707d-3c5b-404e-aa2f-e13092ac8d95
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b13ddc498962ca23e6bc1f5e7a10d88af47ff7d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058873"
---
# <a name="fast-parse"></a>Fast Parse
  快速剖析提供一組快速、簡單的常式用以剖析資料。 這些常式並不區分地區設定，而且只支援一組日期、時間和整數格式的子集。  
  
## <a name="requirements-and-limitations"></a>需求和限制  
 實作快速剖析時，封裝將無法解譯使用特定地區設定格式與許多常用之 ISO 8601 基本格式與擴充格式的日期、時間和數值資料，但卻可以提高封裝的效能。 例如，快速剖析僅支援最常用的日期格式表示法 (例如 YYYYMMDD 和 YYYY-MM-DD)，不會執行地區設定特定的剖析，也不會識別貨幣資料中的特殊字元，且無法轉換以十六進位表示或以科學記號表示的整數。  
  
 只有在使用「一般檔案」來源或「資料轉換」時，才能夠使用快速剖析。 效能的提高可能會很顯著，因此如果可能，您應該考慮在這些資料流程元件中使用快速剖析。  
  
 如果封裝中的資料流程需要區分地區設定的剖析，則建議使用標準剖析來代替快速剖析。 例如，快速剖析不會識別區分地區設定的資料，包括十進位符號 (例如逗號)、非年-月-日格式的日期格式以及貨幣符號。  
  
 快速剖析不會識別隱含一或多個日期部分 (例如紀元、年或月) 的截斷表示法。 例如，快速剖析無法識別以隱含紀元方式指定年份和月份的 '**-YYMM**' 格式，也無法識別以隱含年份方式指定月份的 '**--MM**' 格式。 不過，可以識別已降低有效位數的某些表示法。 例如，快速剖析可識別僅指出小時和分鐘的「hhmm;」格式，以及僅指出年份的「**YYYY**」格式。  
  
 快速剖析在資料行層級指定。 在「一般檔案」來源和「資料轉換」轉換中，可以在輸出資料行上指定「快速剖析」。 輸入和輸出均可包含區分地區設定和不區分地區設定的資料行。  
  
 如需有關「快速剖析」支援之資料格式的詳細資訊，請參閱＜ [Numeric Data Formats](../../2014/integration-services/numeric-data-formats.md) ＞及＜ [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
 [設定快速剖析](../../2014/integration-services/set-fast-parse.md)  
  
  
