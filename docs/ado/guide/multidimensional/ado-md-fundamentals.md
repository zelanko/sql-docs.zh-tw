---
description: ADO MD 基本概念
title: ADO MD 基礎 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: rothja
ms.author: jroth
ms.openlocfilehash: fec7d924003df2a0c0c20b5ca2b0de9162cfd1c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452440"
---
# <a name="ado-md-fundamentals"></a>ADO MD 基本概念
Microsoft® (多維度)  (ADO MD) 的 ActiveX®資料物件，可讓您輕鬆存取來自 Microsoft Visual Basic® Microsoft Visual C++®等語言的多維度資料。 ADO MD 將 Microsoft ActiveX®資料物件延伸 (ADO) ，以包含多維度資料的特定物件，例如 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 和資料 [格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 物件。 您可以使用 ADO MD 流覽多維度架構、查詢 cube，以及取得結果。  
  
 如同 ADO，ADO MD 會使用基礎 OLE DB 提供者來取得資料的存取權。 若要使用 ADO MD，提供者必須是由 OLAP 規格 OLE DB 所定義的多維度資料提供者 (MDP) 。 MDP 會以多維度視圖來呈現資料，而不是表格式視圖，這是表格式資料提供者 (TDP) 呈現資料的方式。 請參閱 OLAP OLE DB 提供者的檔，以取得提供者所支援之特定語法和行為的詳細資訊。  
  
 本檔假設您已瞭解 Visual Basic 程式設計語言，以及 ADO 和 OLAP 的一般知識。 如需詳細資訊，請參閱 ADO 程式設計 [人員指南](../../../ado/guide/ado-programmer-s-guide.md) ，以及 [線上分析處理 (OLAP) 的 OLE DB ](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)。  
  
 此章節包含下列主題。  
  
-   [多維度結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)   
 [資料定義語言和安全性的 ADO 延伸模組 (ADOX) ](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多維度架構和資料的總覽](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 搭配 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
