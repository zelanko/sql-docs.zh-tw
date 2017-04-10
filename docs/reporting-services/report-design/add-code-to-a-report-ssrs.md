---
title: "將程式碼加入至報表 (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "程式碼 [Reporting Services]"
  - "自訂程式碼 [Reporting Services]"
  - "運算式 [Reporting Services]，程式碼"
  - "加入程式碼"
  - "報表 [Reporting Services]，程式碼"
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
caps.latest.revision: 41
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 41
---
# 將程式碼加入至報表 (SSRS)
  在任何運算式中，您可以呼叫自己的自訂程式碼。 您可以透過下列兩個方法來提供程式碼：  
  
-   將以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 撰寫的程式碼直接內嵌在報表中。 如果程式碼參考的是非 <xref:System.Math> 或 <xref:System.Convert> 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，您即必須在報表中加入參考。 如需詳細資訊，請參閱 [Add an Assembly Reference to a Report &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md) (將組件參考加入至報表 (SSRS))。 如需可從程式碼建立之其他參考的詳細資訊，請參閱 [Custom Code and Assembly References in Expressions in Report Designer &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md) (報表設計師中運算式的自訂程式碼及組件參考 (SSRS))。  
  
-   藉由使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]來提供自訂程式碼組件。 如果您提供自訂組件，您必須同時將它安裝在您撰寫報表的電腦上及檢視報表的報表伺服器上。 如需詳細資訊，請參閱 [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)。  
  
### 將內嵌程式碼加入報表中  
  
1.  在 [設計] 檢視中，以滑鼠右鍵按一下報表框線外面的設計介面，然後按一下 [報表屬性]。  
  
2.  按一下 **[程式碼]**。  
  
3.  在 **[自訂程式碼]**中，輸入程式碼。 當報表執行時，程式碼中的錯誤會產生警告。 下列範例會建立名為 `ChangeWord` 的自訂函數，以 "`Bike`" 取代 "`Bicycle`" 一字。  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  下列範例示範如何在運算式中將名為 Category 的資料集欄位傳遞給這個函數：  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     如果您將此運算式加入至顯示類別目錄值的資料表資料格，則每當 "Bike" 一字位於該資料列的資料集欄位中時，此資料表資料格值就會改為顯示 "Bicycle" 一字。  
  
## 請參閱＜  
 [報表屬性對話方塊、程式碼](../Topic/Report%20Properties%20Dialog%20Box,%20Code.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/parameters-collection-references-report-builder-and-ssrs.md)  
  
  