---
title: ADOX 基礎 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5350fd4c4fd8fc447f3987ad502c49a2704e6762
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836436"
---
# <a name="adox-fundamentals"></a>ADOX 基本概念
Microsoft® ActiveX® 資料物件的擴充功能資料定義語言和安全性 (ADOX) 是 ADO 物件和程式設計模型的擴充功能。 ADOX 包含物件的結構描述建立和修改，以及安全性。 因為它是以結構描述管理物件為基礎的方法，您可以撰寫程式碼，能針對各種資料來源，不論其原生的語法差異。  
  
 ADOX 是同一系列文件庫到核心 ADO 物件。 它會公開建立、 修改和刪除結構描述物件，例如資料表和程序的其他物件。 它也包含安全性物件，來維持使用者和群組，並授與及撤銷的物件權限。  
  
 若要使用您的開發工具中的 ADOX，您應該建立 ADOX 型別程式庫的參考。 ADOX 程式庫的描述是 「 Microsoft ADO DDL 和安全性的分機。 」 ADOX 程式庫檔案名稱 Msadox.dll，且程式識別碼 (ProgID) 是 「 ADOX"。 如需有關如何建立程式庫參考的詳細資訊，請參閱您的開發工具的文件。  
  
 Microsoft OLE DB Provider for Microsoft Jet 資料庫引擎完全支援 ADOX。 ADOX 的某些功能可能不支援，視您的資料提供者而定。  
  
 本文件假設您已經具備的 Microsoft® Visual Basic® 程式設計語言和 ADO 的一般知識。 如需有關 ADO 的詳細資訊，請參閱[ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)。 ADOX 有關的詳細概觀資訊，請參閱下列主題：  
  
-   [ADOX 物件模型](../../../ado/reference/adox-api/adox-object-model.md)  
  
-   [ADOX 物件](../../../ado/reference/adox-api/adox-objects.md)  
  
-   [ADOX 集合](../../../ado/reference/adox-api/adox-collections.md)  
  
-   [ADOX 屬性](../../../ado/reference/adox-api/adox-properties.md)  
  
-   [ADOX 方法](../../../ado/reference/adox-api/adox-methods.md)  
  
-   [ADOX 範例](../../../ado/reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX API 參考](../../../ado/reference/adox-api/adox-api-reference.md)   
 [ADOX 程式碼範例](../../../ado/reference/adox-api/adox-code-examples.md)   
 [ADOX 集合](../../../ado/reference/adox-api/adox-collections.md)   
 [ADOX 列舉常數](../../../ado/reference/adox-api/adox-enumerated-constants.md)   
 [ADOX 方法](../../../ado/reference/adox-api/adox-methods.md)   
 [ADOX 物件模型](../../../ado/reference/adox-api/adox-object-model.md)   
 [ADOX 物件](../../../ado/reference/adox-api/adox-objects.md)   
 [ADOX 屬性](../../../ado/reference/adox-api/adox-properties.md)   
 [ADO （多維度） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)
