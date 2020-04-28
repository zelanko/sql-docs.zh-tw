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
ms.openlocfilehash: 541c92cd34b9cbaecdd1001be29dbab8d9b194a0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922417"
---
# <a name="rds-tutorial"></a>RDS 教學課程
本教學課程說明如何使用 RDS 程式設計模型來查詢和更新資料來源。 首先，它會說明完成這項工作所需的步驟。 然後，本教學課程會在 Microsoft® Visual Basic Scripting Edition 中重複（採用適用于 Windows Foundation 類別的 ADO （ADO/WFC））。  
  
 本教學課程是以不同的語言編碼，原因有兩個：  
  
-   RDS 的檔會假設 Visual Basic 中的讀取器程式碼。 這可讓 Visual Basic 程式設計人員方便使用，但較不適用於使用其他語言的程式設計人員。  
  
-   如果您不確定特定的 RDS 功能並知道另一種語言，您可以藉由尋找以另一種語言表示的相同功能，來解決您的問題。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="how-the-tutorial-is-presented"></a>教學課程的呈現方式  
 本教學課程是以 RDS 程式設計模型為基礎。 它會個別討論程式設計模型的每個步驟。 此外，它也會以 Visual Basic 程式碼片段說明每個步驟。  
  
 程式碼範例會以其他語言重複，並進行最少的討論。 給定程式設計語言教學課程中的每個步驟都會以程式設計模型和描述性教學課程中的對應步驟來標示。 使用步驟的編號來參考描述性教學課程中的討論。  
  
 RDS 程式設計模型會在下一節中注明。 當您繼續進行本教學課程時，請使用它作為藍圖。  
  
## <a name="rds-programming-model-with-objects"></a>具有物件的 RDS 程式設計模型  
  
-   指定要在伺服器上叫用的程式，並從用戶端取得方法（proxy）來參考它。  
  
-   叫用伺服器程式。 將參數傳遞給識別資料來源的伺服器程式，以及要發出的命令。  
  
-   伺服器程式會從資料來源取得[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，通常是使用 ADO。 （選擇性）在伺服器上處理**記錄集**物件。  
  
-   伺服器程式會將最終的**記錄集**物件傳回至用戶端應用程式。  
  
-   在用戶端上，**記錄集**物件可以選擇性地放入表單中，供視覺控制項輕鬆使用。  
  
-   對**記錄集**物件所做的變更會傳送回伺服器，用來更新資料來源。  
  
 本教學課程包含下列主題。  
  
-   [步驟 1：指定伺服器程式 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [步驟 2：叫用伺服器程式 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [步驟 3：伺服器取得資料錄集 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [步驟 4：伺服器傳回資料錄集 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [步驟 5：將 DataControl 設為可用 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [步驟 6：將變更傳送到伺服器 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>另請參閱  
 [步驟1：指定伺服器程式（RDS 教學課程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
