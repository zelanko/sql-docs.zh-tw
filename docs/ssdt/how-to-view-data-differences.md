---
title: 如何：檢視資料差異 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.f1
ms.assetid: f88d3350-2eaf-44cc-96a8-84008b6cd071
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c913ffa52c07091e4eec45f6013a3540edfe810
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614260"
---
# <a name="how-to-view-data-differences"></a>如何：檢視資料差異
當您比較兩個資料庫的資料之後，會看到所比較的每個資料庫物件及其狀態。 您也可以檢視每個物件內記錄的結果 (依狀態分組)。  
  
當您檢視差異之後，可以針對不同、遺漏或新增的部分或所有物件或記錄，更新目標以符合來源。  
  
### <a name="to-view-data-differences"></a>若要檢視資料差異  
  
1.  比較來源和目標的資料。  
  
2.  (選擇性) 執行下列其中一項或兩項作業：  
  
    -   根據預設，不論其狀態，所有物件的結果都會顯示。 若只要顯示具有特定狀態的物件，請按一下 [篩選] 清單中的選項。  
  
    -   若要檢視在特定物件內記錄的結果，請按一下主要結果窗格中的物件，然後按一下 [記錄檢視] 窗格中的索引標籤。 每個索引標籤會顯示該物件中具有特定狀態的所有記錄：不同、僅限於來源、僅限於目標和相同。 資料會以記錄和資料行顯示。  
  
## <a name="see-also"></a>另請參閱  
[如何：使用結構描述比較，比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
