---
title: ADO MD 基本概念 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf6cf507d47527e2ca6a72985b6f5bc817ba88e7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273507"
---
# <a name="ado-md-fundamentals"></a>ADO MD 基本概念
Microsoft® ActiveX® Data Objects （多維度） (ADO MD) 提供簡易存取多維度資料的語言 Microsoft Visual Basic®，例如從 microsoft。 ADO MD 擴充 Microsoft ActiveX® Data Objects (ADO) 要包含物件的特定多維度資料，例如[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)和[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。 使用 ADO MD 中，您可以瀏覽多維度結構描述、 查詢 cube 中，並擷取結果。  
  
 ADO 中，例如 ADO MD 會使用基礎的 OLE DB 提供者來存取資料。 若要使用 ADO MD 中，提供者必須是 OLE DB for OLAP 規格所定義的多維度資料提供者 (MDP)。 MDP 提供資料在多維度的檢視，而不要使用表格式檢視，這是表格式資料提供者 (TDP) 如何呈現資料。 請參閱您的 OLAP OLE DB 提供者，如需有關的特定語法與您的提供者所支援的行為的文件。  
  
 本文假設您使用 Visual Basic 程式語言的知識和 ADO 和 OLAP 的一般知識。 如需詳細資訊，請參閱[ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)和[OLE DB 的線上分析處理 (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)。  
  
 此章節包含下列主題。  
  
-   [多維度結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)   
 [ADO 的擴充功能資料定義語言和安全性 (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多維度結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 搭配 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
