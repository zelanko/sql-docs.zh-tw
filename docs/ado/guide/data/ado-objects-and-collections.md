---
title: ADO 物件和集合 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 795c9aa81c70085396d7650484fa3e5b5d445504
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="ado-objects-and-collections"></a>ADO 物件和集合
ADO 是由下列九個物件和四個集合所組成。  
  
|物件或集合|Description|  
|--------------------------|-----------------|  
|**連接**物件|代表資料來源的唯一工作階段。 在用戶端/伺服器資料庫系統，可能相當於實際的網路連線到伺服器。 根據提供者、 某些集合、 方法或屬性所支援的功能**連接**物件可能無法使用。|  
|**Command** 物件|用來定義特定的命令，例如 SQL 查詢，要針對資料來源執行。|  
|**資料錄集**物件|代表完整記錄的基底資料表或執行的命令的結果。 所有**資料錄集**物件所組成 （資料列） 的記錄和欄位 （資料行）。|  
|**記錄**物件|代表單一資料列的資料，從**資料錄集**或從提供者。 資料庫記錄或其他類型的物件，例如檔案或目錄，您的提供者而定，可能表示此記錄。|  
|**資料流**物件|代表二進位或文字資料的資料流。 例如，XML 文件可以載入命令輸入或當做查詢的結果，從某些提供者傳回的資料流。 A**資料流**物件可以用來操作欄位或記錄包含這些資料流的資料。|  
|**參數**物件|代表參數或相關聯的引數**命令**參數型的查詢或預存程序為基礎的物件。|  
|**欄位**物件|代表具有通用的資料類型的資料行。 每個**欄位**物件對應中的資料行**資料錄集**。|  
|**屬性**物件|代表 ADO 物件提供者所定義的特性。 ADO 物件有兩種類型的屬性： 內建和動態。 內建屬性是在 ADO 和立即提供給任何新物件實作這些屬性。 **屬性**物件是容器的基礎提供者所定義的動態屬性。|  
|**Error** 物件|包含關於涉及提供者的單一作業相關的資料存取錯誤的詳細資料。|  
|**欄位**集合|包含所有**欄位**物件**資料錄集**或**記錄**物件。|  
|**屬性**集合|包含所有**屬性**物件的特定執行個體的物件。|  
|**參數**集合|包含所有**參數**物件**命令**物件。|  
|**錯誤**集合|包含所有**錯誤**為了回應單一提供者相關的失敗所建立的物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)
