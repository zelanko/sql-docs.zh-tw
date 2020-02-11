---
title: ADOX 基本概念 |Microsoft Docs
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
ms.openlocfilehash: 66965b99d0f8bcc87025239f7ffa54814e6d74f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923266"
---
# <a name="adox-fundamentals"></a>ADOX 基本概念
Microsoft®適用于資料定義語言和安全性的 ActiveX®資料物件延伸模組（ADOX）是 ADO 物件和程式設計模型的延伸。 ADOX 包含用於建立和修改架構的物件，以及安全性。 因為它是以物件為基礎的架構操作方法，所以您可以撰寫程式碼來處理各種資料來源，而不論其原生語法有何差異。  
  
 ADOX 是核心 ADO 物件的附屬程式庫。 它會公開用來建立、修改和刪除架構物件（例如資料表和程式）的其他物件。 它也包含安全性物件，可維護使用者和群組，以及授與及撤銷物件的許可權。  
  
 若要搭配使用 ADOX 與您的開發工具，您應該建立 ADOX 類型程式庫的參考。 ADOX 程式庫的描述為「Microsoft ADO Ext，適用于 DDL 和安全性」。 ADOX 程式庫檔案名為 Msadox，而程式識別碼（ProgID）為 "ADOX"。 如需建立程式庫參考的詳細資訊，請參閱開發工具的檔。  
  
 Microsoft Jet 資料庫引擎的 Microsoft OLE DB 提供者完全支援 ADOX。 視您的資料提供者而定，可能不支援 ADOX 的某些功能。  
  
 本檔假設您已瞭解 Microsoft® Visual Basic®程式設計語言，以及 ADO 的一般知識。 如需 ADO 的詳細資訊，請參閱 Ado 程式設計[人員指南](../../../ado/guide/ado-programmer-s-guide.md)。 如需 ADOX 的詳細總覽資訊，請參閱下列主題：  
  
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
 [ADO （多維度）（ADO MD）](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)
