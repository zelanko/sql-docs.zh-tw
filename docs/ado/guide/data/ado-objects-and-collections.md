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
ms.openlocfilehash: 89093367532177ec87fb3a5fd86e38e98345962c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926046"
---
# <a name="ado-objects-and-collections"></a>ADO 物件和集合
ADO 包含下列九個物件和四個集合。  
  
|物件或集合|描述|  
|--------------------------|-----------------|  
|**Connection**物件|代表資料來源的唯一工作階段。 在用戶端/伺服器資料庫系統的情況下，它可能相當於與伺服器的實際網路連接。 視提供者支援的功能而定，可能無法使用**連接**物件的某些集合、方法或屬性。|  
|**Command**物件|用來定義特定的命令，例如要針對資料來源執行的 SQL 查詢。|  
|**Recordset**物件|代表基表的整組記錄或已執行命令的結果。 所有記錄**集**物件都是由記錄（資料列）和欄位（資料行）所組成。|  
|**Record**物件|表示單一資料列，不論是從**記錄集**或提供者。 此記錄可能代表資料庫記錄或其他類型的物件（例如檔案或目錄），視您的提供者而定。|  
|**Stream**物件|表示二進位或文字資料的資料流程。 例如，您可以將 XML 檔載入資料流程以進行命令輸入，或從特定提供者傳回做為查詢的結果。 **資料流程**物件可以用來操作包含這些資料資料流程的欄位或記錄。|  
|**Parameter**物件|根據參數化查詢或預存程式，表示與**命令**物件相關聯的參數或引數。|  
|**Field**物件|表示具有 common 資料類型的資料行。 每個**Field**物件都會對應至**記錄集**內的資料行。|  
|**Property**物件|表示由提供者定義之 ADO 物件的特性。 ADO 物件有兩種屬性類型：內建和動態。 內建屬性是在 ADO 中實作為並可立即提供給任何新物件的屬性。 **屬性**物件是動態屬性的容器，由基礎提供者所定義。|  
|**Error**物件|包含有關與提供者的單一作業相關之資料存取錯誤的詳細資訊。|  
|**Fields**集合|包含**記錄集**或**記錄**物件的所有**欄位**物件。|  
|**Properties**集合|包含物件之特定實例的所有**屬性**物件。|  
|**Parameters**集合|包含**Command**物件的所有**參數**物件。|  
|**錯誤**集合|包含為了回應單一提供者相關的失敗所建立的所有**錯誤**物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)
