---
title: 使用 ADO 搭配 ADO MD |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d6aed08b40b25eb0f725697eb6fac8908894ebd
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273529"
---
# <a name="using-ado-with-ado-md"></a>使用 ADO 搭配 ADO MD
ADO 和 ADO MD 個相關但不同的物件模型。 ADO 提供物件連接到資料來源、 執行命令、 擷取表格式資料和結構描述中繼資料，以表格格式，以及檢視提供者資訊時發生錯誤。 ADO MD 可用於擷取多維度資料和多維度結構描述中繼資料檢視的物件。  
  
 當您使用 MDP 時，您可以選擇使用 ADO、 ADO MD 中，或兩者皆擁有您的應用程式。 藉由參考您的專案內的兩個程式庫，您將擁有完整存取權您 MDP 提供的功能。  
  
 它會取用者，以取得多維度資料集的簡維、 表格式檢視通常很有用。 您可以使用 ADO[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 指定的來源您[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)為***來源***參數[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**資料錄集**，而不是做為來源ADO MD**資料格集**。  
  
 它也可能可以在表格式檢視中，而不是物件的階層架構檢視結構描述中繼資料。 ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件可讓使用者開啟**資料錄集**，其中包含結構描述資訊。 ***QueryType***參數**OpenSchema**方法有數個[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) MDPs 相關的值。 這些值如下所述：  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 若要使用 ADO MD 屬性或方法的 ADO 列舉值，您的專案必須參考 ADO 和 ADO MD 程式庫。 例如，您可以使用 ADO **adState**列舉值使用 ADO MD[狀態](../../../ado/reference/ado-md-api/state-property-ado-md.md)屬性。 如需如何建立程式庫的參考的詳細資訊，請參閱您的開發工具的文件。  
  
 如需 ADO 物件和方法的詳細資訊，請參閱[ADO 應用程式開發介面參考](../../../ado/reference/ado-api/ado-api-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多維度結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
