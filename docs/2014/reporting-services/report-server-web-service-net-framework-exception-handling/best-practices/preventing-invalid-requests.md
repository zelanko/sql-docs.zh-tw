---
title: 防止無效的要求 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dcb850ad7e99768781b225978f531ff991766924
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158964"
---
# <a name="preventing-invalid-requests"></a>防止無效的要求
  您可以防止擲回某些類型的例外狀況，方法是分析應用程式流程，並確保傳送到報表伺服器的要求是有效的。 例如，在可讓使用者加入或更新報表名稱、資料來源或是其他報表伺服器項目的應用程式中，您應該驗證使用者可能輸入的文字。 傳送要求到報表伺服器之前，請務必檢查保留字元。 請使用 **if** 條件陳述式或程式碼中的其他邏輯建構來警示使用者，告知使用者他們未符合傳送要求到報表伺服器所需的條件。  
  
 在下列簡化的 C# 範例中，當使用者嘗試使用包含斜線 (/) 字元的名稱來建立報表時，會顯示易懂的錯誤訊息。  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 如需將要求傳送到報表伺服器之前可以避免之錯誤類型的詳細資訊，請參閱 [SoapException 錯誤資料表](../soapexception-class/soapexception-errors-table.md)。 如需使用 Try/Catch 區塊進一步加強上述範例的詳細資訊，請參閱[使用 Try 和 Catch 區塊](using-try-and-catch-blocks.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
