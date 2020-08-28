---
description: ADO 物件和集合
title: ADO 物件和集合 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: rothja
ms.author: jroth
ms.openlocfilehash: 04985c3972e9eaa1ec854102123c09c6a3fd8cde
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991639"
---
# <a name="ado-objects-and-collections"></a>ADO 物件和集合
ADO 是由下列九個物件和四個集合所組成。  
  
|物件或集合|描述|  
|--------------------------|-----------------|  
|**Connection** 物件|代表資料來源的唯一工作階段。 如果是用戶端/伺服器資料庫系統，則可能相當於與伺服器的實際網路連接。 視提供者支援的功能而定，可能無法使用 **連接** 物件的某些集合、方法或屬性。|  
|**Command** 物件|用來定義要針對資料來源執行的特定命令（例如 SQL 查詢）。|  
|**Recordset** 物件|表示基表中的整組記錄，或執行命令的結果。 所有 **記錄集** 物件都包含記錄 (資料列) 和欄位 (資料行) 。|  
|**Record** 物件|表示單一資料列，不論是從 **記錄集** 或提供者。 這項記錄可能代表資料庫記錄或其他類型的物件（例如檔案或目錄），視您的提供者而定。|  
|**Stream** 物件|表示二進位或文字資料的資料流程。 例如，XML 檔可以載入命令輸入的資料流程中，或從特定提供者傳回做為查詢的結果。 **資料流程**物件可以用來操作包含這些資料資料流程的欄位或記錄。|  
|**Parameter** 物件|根據參數化查詢或預存程式，表示與 **Command** 物件相關聯的參數或引數。|  
|**Field** 物件|表示具有通用資料類型之資料的資料行。 每個 **Field** 物件都會對應到 **記錄集中**的資料行。|  
|**Property** 物件|表示由提供者定義之 ADO 物件的特性。 ADO 物件有兩種類型的屬性：內建和動態。 內建屬性是在 ADO 中執行的屬性，而且可立即提供給任何新的物件使用。 **屬性**物件是動態屬性的容器，由基礎提供者定義。|  
|**Error** 物件|包含有關與提供者的單一作業相關之資料存取錯誤的詳細資料。|  
|**Fields** 集合|包含**記錄集**或**記錄**物件的所有**欄位**物件。|  
|**Properties** 集合|包含物件之特定實例的所有 **屬性** 物件。|  
|**Parameters** 集合|包含**Command**物件的所有**參數**物件。|  
|**錯誤** 集合|包含為了回應單一提供者相關的失敗而建立的所有 **錯誤** 物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO 物件模型](../../reference/ado-api/ado-object-model.md)