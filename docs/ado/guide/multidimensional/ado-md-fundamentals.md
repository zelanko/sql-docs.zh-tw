---
title: ADO MD 基本概念 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bbff704e174dd824eca7b1f71c8f9d3fc15def51
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704419"
---
# <a name="ado-md-fundamentals"></a>ADO MD 基本概念
Microsoft® ActiveX® Data Objects （多維度） (ADO MD) 可輕鬆存取多維度資料的語言，例如 Microsoft Visual Basic®，Microsoft Visual C++®。 ADO MD 擴充 Microsoft ActiveX® Data Objects (ADO) 使其包含專屬於多維度資料，例如[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)並[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。 使用 ADO MD 中，您可以瀏覽多維度的結構描述、 查詢 cube，並擷取結果。  
  
 ADO 中，例如 ADO MD 使用基礎的 OLE DB 提供者來存取資料。 若要使用 ADO MD，OLE DB for OLAP 規格所定義的提供者時，必須為多維度資料提供者 (MDP)。 MDP 提供多維度的檢視，而不是表格式檢視中的資料，這是表格式資料提供者 (TDP) 如何呈現資料。 請參閱文件以取得您的 OLAP OLE DB 提供者，如需有關的特定語法與您的提供者所支援的行為。  
  
 本文件假設使用 Visual Basic 程式設計語言的知識和 ADO 和 OLAP 的一般知識。 如需詳細資訊，請參閱 < [ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)並[OLE DB 的線上分析處理 (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)。  
  
 此章節包含下列主題。  
  
-   [多維度結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)   
 [ADO 延伸模組的資料定義語言和安全性 (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多維度的結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
