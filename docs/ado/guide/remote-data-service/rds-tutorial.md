---
title: "RDS 教學課程 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6cfb12781ca9e7387ea8016de581217ddf95f9c1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="rds-tutorial"></a>RDS 教學課程
本教學課程說明如何使用查詢及更新資料來源的 RDS 程式設計模型。 首先，它會描述完成這項工作所需的步驟。 本教學課程會重複在 Microsoft® Visual Basic Scripting Edition （包括 ADO 的 Windows Foundation Classes (ADO/WFC)）。  
  
 本教學課程以不同的語言編碼，原因有兩個：  
  
-   RDS 的文件會假設在 Visual Basic 中的讀取器程式碼。 這可讓文件方便的 Visual Basic 程式設計人員，但較沒有用的程式設計人員使用其他語言。  
  
-   如果您不確定特定 RDS 功能，有了另一種語言，您可以藉由尋找另一種語言中表示的相同功能來解決您的問題。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="how-the-tutorial-is-presented"></a>本教學課程的呈現方式  
 本教學課程根據 RDS 的程式設計模型。 其中也會個別討論每個步驟的程式設計模型。 此外，它會說明每個步驟的 Visual Basic 程式碼片段。  
  
 程式碼範例會以最少的討論與其他語言重複。 程式設計模型和描述性的教學課程中，給定的程式設計語言教學課程中的每個步驟會標示為對應步驟。 使用步驟的數目，來參照描述性的教學課程中的討論。  
  
 下一節中所述的 RDS 的程式設計模型。 將它當做藍圖當您進行本教學課程。  
  
## <a name="rds-programming-model-with-objects"></a>RDS 與物件的程式設計模型  
  
-   指定要在伺服器上，叫用的程式，並取得用戶端從參考它的方式 (proxy)。  
  
-   叫用伺服器程式。 將參數傳遞至伺服器程式的識別資料來源以及要發出的命令。  
  
-   伺服器程式會取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)來自資料來源，通常是透過使用 ADO 的物件。 （選擇性）**資料錄集**物件在伺服器上處理。  
  
-   伺服器程式傳回最終**資料錄集**用戶端應用程式的物件。  
  
-   在用戶端，**資料錄集**物件會選擇性地放入容易使用的視覺控制項的表單。  
  
-   若要變更**資料錄集**物件傳送至伺服器及用來更新資料來源。  
  
 本教學課程包含下列主題。  
  
-   [步驟 1：指定伺服器程式 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [步驟 2：叫用伺服器程式 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [步驟 3：伺服器取得資料錄集 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [步驟 4：伺服器傳回資料錄集 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [步驟 5：將 DataControl 設為可用 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [步驟 6：將變更傳送到伺服器 (RDS 教學課程)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>另請參閱  
 [步驟 1： 指定程式的伺服器 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

