---
title: RDS 教學課程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c9136f1fc1fdf7538744501984af50e2ca52f04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929883"
---
# <a name="rds-tutorial"></a>RDS 教學課程
本教學課程說明如何使用 RDS 程式設計模型來查詢及更新資料來源。 首先，它會描述要完成這項工作所需的步驟。 則教學課程中重複出現在 Microsoft® Visual Basic Scripting Edition （具備 ADO 的 Windows Foundation Classes (ADO/WFC)）。  
  
 本教學課程會以不同的語言編碼，原因有兩個：  
  
-   RDS 的文件會假設讀取器程式碼，在 Visual Basic 中。 這可讓文件方便 Visual Basic 程式設計人員，但較沒有用的程式設計人員使用其他語言。  
  
-   如果您不確定特定的 RDS 功能資料，而且有了另一種語言，您可以尋找另一種語言來表示相同的功能來解決您的問題。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="how-the-tutorial-is-presented"></a>本教學課程的呈現方式  
 本教學課程為基礎的 RDS 程式設計模型。 它會個別討論的程式設計模型的每個步驟。 此外，它會說明每個步驟的 Visual Basic 程式碼片段。  
  
 在程式碼範例會在最少討論其他語言重複。 程式設計模型和描述性的教學課程中，在指定的程式設計語言教學課程中的每個步驟會標示為對應的步驟。 使用步驟的數目表示描述性的教學課程中的討論。  
  
 RDS 程式設計模型是由下列一節所述。 使用 azure 藍圖為您進行教學課程。  
  
## <a name="rds-programming-model-with-objects"></a>具有物件的 RDS 程式設計模型  
  
-   指定要在伺服器上，叫用的程式，並取得用戶端從參考它的方式 (proxy)。  
  
-   叫用伺服器程式。 將參數傳遞至伺服器程式識別資料來源以及要發出的命令。  
  
-   伺服器程式會取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從資料來源，通常是藉由使用 ADO 的物件。 （選擇性）**資料錄集**物件在伺服器上處理。  
  
-   伺服器程式會傳回最後**資料錄集**用戶端應用程式的物件。  
  
-   在用戶端**資料錄集**物件會選擇性地放入容易使用的視覺控制項的表單。  
  
-   若要變更**資料錄集**物件傳送至伺服器及用來更新資料來源。  
  
 本教學課程包含下列主題。  
  
-   [步驟 1：指定的伺服器程式 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [步驟 2：叫用伺服器程式 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [步驟 3：伺服器會取得資料錄集 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [步驟 4：伺服器會傳回資料錄集 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [步驟 5：DataControl 設為可用 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [步驟 6：變更傳送到伺服器 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>另請參閱  
 [步驟 1：指定的伺服器程式 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
