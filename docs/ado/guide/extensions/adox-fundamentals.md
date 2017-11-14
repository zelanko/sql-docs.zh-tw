---
title: "ADOX 基本概念 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dbc8d415e4dfcaeb4bf7e6a489bd407e87335874
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="adox-fundamentals"></a>ADOX 基本概念
Microsoft® ActiveX® 資料物件的擴充功能資料定義語言和安全性 (ADOX) 是程式設計模型與 ADO 物件的擴充功能。 ADOX 包含物件的結構描述建立和修改，以及安全性。 因為它是以結構描述管理物件為基礎的方法，您可以撰寫程式碼會針對各種資料來源，不論其原生的語法差異。  
  
 ADOX 是核心 ADO 物件的附屬文件庫。 它會公開其他物件的建立、 修改和刪除結構描述物件，例如資料表和程序。 它也維持使用者和群組，並且將授與及撤銷權限物件的安全性物件。  
  
 若要使用 ADOX 與開發工具，您應該建立 ADOX 類型程式庫的參考。 ADOX 文件庫的描述是 「 Microsoft ADO 外部 DDL 和安全性。 」 ADOX 程式庫檔案名稱 Msadox.dll，且程式識別碼 (ProgID) 是 「 ADOX"。 如需有關如何建立程式庫的參考的詳細資訊，請參閱您的開發工具的文件。  
  
 Microsoft OLE DB Provider for Microsoft Jet 資料庫引擎完全支援 ADOX。 ADOX 的某些功能可能不支援，視您的資料提供者而定。  
  
 本文件假設您已經具備的 Microsoft® Visual Basic® 程式設計語言和 ADO 的一般知識。 如需 ADO 的詳細資訊，請參閱[ADO 程式設計人員指南](../../../ado/guide/ado-programmer-s-guide.md)。 如需 ADOX 相關的概觀資訊，請參閱下列主題：  
  
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

