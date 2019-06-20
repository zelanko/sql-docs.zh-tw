---
title: ADO 物件和集合 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 62616ecebb8fa7795462c7e22437aabebb56bcaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700959"
---
# <a name="ado-objects-and-collections"></a>ADO 物件和集合
ADO 是由下列九個物件和四個集合所組成。  
  
|物件或集合|描述|  
|--------------------------|-----------------|  
|**連接**物件|代表資料來源的唯一工作階段。 在用戶端/伺服器資料庫系統，可能會相當於實際的網路連線到伺服器。 根據提供者、 某些集合、 方法或屬性所支援的功能**連線**物件可能無法使用。|  
|**Command** 物件|用來定義特定的命令，例如 SQL 查詢，用來針對資料來源執行。|  
|**資料錄集**物件|代表整個記錄集的基底資料表或執行命令的結果。 所有**資料錄集**物件所組成 （資料列） 的記錄和欄位 （資料行）。|  
|**記錄**物件|表示單一資料列的資料，從**資料錄集**或從提供者。 此記錄可能代表資料庫記錄或其他類型的物件，例如檔案或目錄，視您的提供者。|  
|**Stream**物件|代表二進位或文字資料流。 例如，XML 文件可以載入的資料流，輸入或從特定提供者傳回為查詢結果的命令。 A **Stream**物件可用來操作欄位或記錄，其中包含這些資料流的資料。|  
|**參數**物件|表示參數或相關聯的引數**命令**參數化的查詢或預存程序為基礎的物件。|  
|**欄位**物件|代表具有通用的資料類型的資料行。 每個**欄位**物件中的資料行對應**資料錄集**。|  
|**屬性**物件|表示提供者會定義於 ADO 物件的特性。 ADO 物件有兩種類型的屬性： 內建和動態。 內建的屬性是在 ADO 和立即提供給任何新的物件來實作這些屬性。 **屬性**物件是基礎提供者所定義的動態屬性的容器。|  
|**Error** 物件|包含屬於單一作業牽涉到提供者的資料存取錯誤的詳細資料。|  
|**欄位**集合|包含所有**欄位**的物件**Recordset**或是**記錄**物件。|  
|**屬性**集合|包含所有**屬性**物件的特定執行個體的物件。|  
|**參數**集合|包含所有**參數**的物件**命令**物件。|  
|**錯誤**集合|包含所有**錯誤**單一提供者相關的失敗回應所建立的物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)
