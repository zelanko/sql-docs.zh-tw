---
description: 搭配 ADO MD 使用 ADO
title: 使用 ADO 搭配 ADO MD |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: rothja
ms.author: jroth
ms.openlocfilehash: b7829b984b603f7b21a339886d956b6db5cc0ffd
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758378"
---
# <a name="using-ado-with-ado-md"></a>搭配 ADO MD 使用 ADO
ADO 和 ADO MD 是相關的，但不同的物件模型。 ADO 提供的物件可連接到資料來源、執行命令、以表格格式抓取表格式資料和架構中繼資料，以及查看提供者錯誤資訊。 ADO MD 提供物件來取得多維度資料和查看多維度架構中繼資料。  
  
 當您使用 MDP 時，您可以選擇在應用程式中使用 ADO、ADO MD 或兩者。 藉由參考專案中的這兩個程式庫，您就可以完整存取 MDP 所提供的功能。  
  
 當取用者取得多維度資料集的簡維表格式視圖時，通常會很有用。 您可以使用 ADO [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件來完成這項作業。 將您的[儲存格](../../reference/ado-md-api/cellset-object-ado-md.md)來源指定為**記錄集**之[Open](../../reference/ado-api/open-method-ado-recordset.md)方法的***來源***參數，而不是 ADO MD**格集**的來源。  
  
 以表格式視圖來查看架構中繼資料，而不是物件的階層架構，也可能很有用。 [Connection](../../reference/ado-api/connection-object-ado.md)物件上的 ADO [OpenSchema](../../reference/ado-api/openschema-method.md)方法可讓使用者開啟包含架構資訊的**記錄集**。 **OpenSchema**方法的***QueryType***參數有數個與 MDPs 相關的[SchemaEnum](../../reference/ado-api/schemaenum.md)值。 這些值如下所述：  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 若要使用 ADO 列舉值搭配 ADO MD 屬性或方法，您的專案必須參考 ADO 和 ADO MD 程式庫。 例如，您可以將 ADO **adState** 列舉值與 ADO MD [State](../../reference/ado-md-api/state-property-ado-md.md) 屬性搭配使用。 如需有關如何建立程式庫參考的詳細資訊，請參閱開發工具的檔。  
  
 如需 ADO 物件和方法的詳細資訊，請參閱 [ADO API 參考](../../reference/ado-api/ado-api-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多維度)  (ADO MD) ](./ado-multidimensional-ado-md.md)   
 [多維度架構和資料的總覽](./overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](./programming-with-ado-md.md)   
 [使用多維度資料](./working-with-multidimensional-data.md)