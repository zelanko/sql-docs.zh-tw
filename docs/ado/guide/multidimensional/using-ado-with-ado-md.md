---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3c634ec056d42e97dcbea3422a0e19a33596d54
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923140"
---
# <a name="using-ado-with-ado-md"></a>搭配 ADO MD 使用 ADO
ADO 和 ADO MD 是相關的，但是不同的物件模型。 ADO 提供連接至資料來源、執行命令、以表格格式抓取表格式資料和架構中繼資料，以及查看提供者錯誤資訊的物件。 ADO MD 提供用來抓取多維度資料和查看多維度架構中繼資料的物件。  
  
 當您使用 MDP 時，您可以選擇在應用程式中使用 ADO、ADO MD 或兩者。 藉由參考專案中的這兩個程式庫，您就可以完整存取 MDP 所提供的功能。  
  
 取用者通常會對多維度資料集取得簡維的表格式視圖，這是很有用的。 您可以使用 ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件來執行這項操作。 將您的資源[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)來源指定為**記錄集**之[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法的***source***參數，而不**是 ADO MD 集**的來源。  
  
 在表格式視圖中查看架構中繼資料，而不是在物件階層中，也可能會很有用。 [Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件上的 ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法可讓使用者開啟包含架構資訊的**記錄集**。 **OpenSchema**方法的***QueryType***參數有數個特別與 MDPs 相關的[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)值。 這些值如下所述：  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 若要使用 ADO 列舉值搭配 ADO MD 屬性或方法，您的專案必須同時參考 ADO 和 ADO MD 程式庫。 例如，您可以使用 ADO **adState**列舉值搭配 ADO MD [State](../../../ado/reference/ado-md-api/state-property-ado-md.md)屬性。 如需如何建立程式庫參考的詳細資訊，請參閱開發工具的檔。  
  
 如需有關 ADO 物件和方法的詳細資訊，請參閱[ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度）（ADO MD）](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多維度架構和資料的總覽](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
