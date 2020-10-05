---
description: RDS 教學課程
title: RDS 教學課程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: rothja
ms.author: jroth
ms.openlocfilehash: 70f91e85010abb784291c3c9eca52b9a74ed6286
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721389"
---
# <a name="rds-tutorial"></a>RDS 教學課程
本教學課程說明如何使用 RDS 程式設計模型來查詢及更新資料來源。 首先，它會說明完成這項工作所需的步驟。 然後，本教學課程會在 Microsoft® Visual Basic Scripting Edition (採用適用于 Windows Foundation 類別的 ADO (ADO/WFC) # A3。  
  
 本教學課程是以不同語言撰寫的程式碼，有兩個原因：  
  
-   RDS 的檔會假設 Visual Basic 中的讀取器程式碼。 這讓檔對 Visual Basic 程式設計人員而言很方便，但較不適合使用其他語言的程式設計人員使用。  
  
-   如果您不確定特定的 RDS 功能，而且您知道有一些其他語言，您可以藉由尋找以另一種語言表示的相同功能來解決問題。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="how-the-tutorial-is-presented"></a>如何呈現教學課程  
 本教學課程是以 RDS 程式設計模型為基礎。 它會個別討論程式設計模型的每個步驟。 此外，它還說明了 Visual Basic 程式碼片段的每個步驟。  
  
 程式碼範例是以其他語言重複進行，最簡單的討論。 給定程式設計語言教學課程中的每個步驟都會標示程式設計模型和描述性教學課程中的對應步驟。 使用步驟的數目來參考描述教學課程中的討論。  
  
 RDS 程式設計模型如下一節所述。 當您繼續進行本教學課程時，請使用它作為藍圖。  
  
## <a name="rds-programming-model-with-objects"></a>具有物件的 RDS 程式設計模型  
  
-   指定要在伺服器上叫用的程式，並取得 (proxy) 從用戶端參考它的方法。  
  
-   叫用伺服器程式。 將參數傳遞給識別資料來源的伺服器程式，以及要發出的命令。  
  
-   伺服器程式會從資料來源取得 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件，通常是使用 ADO。 （選擇性）在伺服器上處理 **記錄集** 物件。  
  
-   伺服器程式會將最終的 **記錄集** 物件傳回至用戶端應用程式。  
  
-   在用戶端上，會選擇性地將 **記錄集** 物件放入可供視覺控制項輕鬆使用的表單中。  
  
-   對 **記錄集** 物件所做的變更會傳送回伺服器，並用來更新資料來源。  
  
 本教學課程包含下列主題。  
  
-   [步驟 1：指定伺服器程式 (RDS 教學課程)](./step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [步驟 2：叫用伺服器程式 (RDS 教學課程)](./step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [步驟 3：伺服器取得資料錄集 (RDS 教學課程)](./step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [步驟 4：伺服器傳回資料錄集 (RDS 教學課程)](./step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [步驟 5：將 DataControl 設為可用 (RDS 教學課程)](./step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [步驟 6：將變更傳送到伺服器 (RDS 教學課程)](./step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 教學課程 (VBScript)](./rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>另請參閱  
 [步驟1：指定伺服器程式 (RDS 教學課程) ](./step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](./rds-tutorial-vbscript.md)