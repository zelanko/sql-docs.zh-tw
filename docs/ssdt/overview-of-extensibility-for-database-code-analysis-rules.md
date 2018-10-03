---
title: 資料庫程式碼分析規則的擴充性概觀 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c754ce006834a44413d64821ea79349da2e62d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699916"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>資料庫程式碼分析規則的擴充性概觀
包含 SQL Server Data Tools 的 Visual Studio 版本包括程式碼分析規則，可報告資料庫程式碼中的 Transact\-SQL 設計、命名和效能警告。 如需詳細資訊，請參閱[分析資料庫程式碼以提升程式碼品質](http://msdn.microsoft.com/library/dd172133(v=vs.100).aspx) \(機器翻譯\)。  
  
如果內建的程式碼分析規則未涵蓋您要包括的特定 Transact\-SQL 問題，則您可以建立自訂的資料庫程式碼分析規則。 例如，您可能想要建立可避免使用 WAITFOR DELAY 陳述式的自訂規則，如[為 SQL Server 編寫自訂靜態程式碼分析規則組件的逐步解說](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md)中所示。 若要建立自訂的資料庫程式碼分析規則，您要使用 [CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx) 命名空間中的類別。  
  
在建立自訂的程式碼分析規則之前，您應該瞭解資料庫程式碼分析規則的各種元件之間的基本架構。  
  
## <a name="database-code-analysis-rules-components"></a>資料庫程式碼分析規則元件  
下圖說明資料庫程式碼分析規則元件如何互動：  
  
![資料庫程式碼分析規則元件](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "資料庫程式碼分析規則元件")  
  
當您使用資料庫程式碼分析規則功能時，無論是直接執行靜態程式碼分析 (如需詳細資訊，請參閱[如何：分析 Transact-SQL 程式碼以找出錯誤](http://msdn.microsoft.com/library/dd172119(v=vs.100).aspx) \(機器翻譯\))，或透過執行建置，都會根據您在專案中設定所有規則的方式來載入並使用它們。 如需詳細資訊，請參閱[如何：啟用和停用資料庫程式碼靜態分析的特定規則](http://msdn.microsoft.com/library/dd172131(v=vs.100).aspx) \(機器翻譯\)。 擴充管理員也將載入您已建立並登錄的任何自訂規則組件。 如需詳細資訊，請參閱[如何：安裝和管理擴充功能](../ssdt/how-to-install-and-manage-feature-extensions.md)。  
  
自訂程式碼分析規則類別繼承自 [SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx)。 自訂規則類別可以透過其規則執行內容來存取許多有用物件。 其中包括：  
  
-   有關規則本身的中繼資料。  
  
-   代表資料庫結構描述的 Dac.Model.TSqlModel，此結構描述包括所有模型元素、這些元素之間的關係，以及元素的任何屬性。  
  
-   對於檢查特定元素的規則，代表模型中該結構描述元素的 Dac.Model.TSqlObject 會包括在內容中。  
  
-   許多結構描述物件也有 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 表示式，可透過此內容存取它 -這是元素的 AST 型表示式，當嘗試查看潛在語法問題，例如出現 [SelectStarExpression](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx) 時，此表示式很有用。  
  
Dac.CodeAnalysis.SqlRuleProblem 是由規則建立，以代表其找到的任何問題。 建立此項時，相關 Dac.Model.TSqlObject 和可能的 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 表示式元素會傳遞至建構函式，而且這些元素會用來判定原始程式碼檔案中發生問題的位置。 分析結束時，這些問題全都會傳遞至錯誤管理員，並顯示在錯誤清單中。  
  
## <a name="see-also"></a>另請參閱  
[擴充資料庫功能](../ssdt/extending-the-database-features.md)  
  
