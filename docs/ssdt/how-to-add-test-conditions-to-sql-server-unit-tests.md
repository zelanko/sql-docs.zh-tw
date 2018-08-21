---
title: 如何：將測試條件加入至 SQL Server 單元測試 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 85ba2e56-a0b2-489c-aea2-fb135cce0cfc
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86e450a6eb6c1e169d5c9dc6147f0ab3cc2a9fb6
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085430"
---
# <a name="how-to-add-test-conditions-to-sql-server-unit-tests"></a>HOW TO：將測試條件加入至 SQL Server 單元測試
您可以使用 [SQL Server 單元測試設計工具]，將測試條件加入至 SQL Server 單元測試。 當您儲存測試類別時，測試條件會以 Visual C\# 或 Visual Basic 程式碼的形式，自動儲存在測試專案的原始程式碼檔案中 (包含測試類別)。 在您儲存測試條件之後，就可以在 [SQL Server 單元測試設計工具] 或其原始程式碼檔案中進行編輯。  
  
### <a name="to-add-test-conditions-to-a-sql-server-unit-test"></a>如何將測試條件加入至 SQL Server 單元測試  
  
1.  在 [SQL Server 單元測試設計工具] 中開啟 SQL Server 單元測試。  
  
    您所開啟之測試的名稱會顯示在 SQL Server 單元測試設計工具最上方的巡覽列中。 您可以使用巡覽列來選取測試類別中的不同測試方法。  
  
2.  在巡覽列中，按一下您想要加入測試條件的測試方法，或按一下 [通用指令碼]。  
  
    > [!NOTE]  
    > 通用指令碼不屬於特定的單元測試。 而是，它們會在測試類別中的單元測試前後執行。 如需詳細資訊，請參閱 [SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)。  
  
3.  在巡覽列中，按一下您想要加入測試條件的 \-SQL 指令碼。 您可以將測試條件加入至測試前、測試或測試後指令碼。  
  
    該項測試的 Transact\-SQL 指令碼會顯示在 Transact\-SQL 編輯器中，而且其測試條件會顯示在 [測試條件] 窗格中。  
  
4.  在 [測試條件] 選擇清單中，按一下測試條件，然後按一下 [加入測試條件] \ (+)。  
  
    測試條件就會加入至單元測試方法。  
  
    > [!NOTE]  
    > 您可以按一下測試條件，然後按一下 [測試條件] 窗格中的向上和向下箭頭，藉以重新排序測試方法中的測試條件。  
  
5.  選取您剛才加入的測試條件並檢視 [屬性] 視窗。  
  
    在 [屬性] 視窗中設定測試條件。 例如，您可以變更執行時間測試條件的 [執行時間] 屬性。 如果您設定此屬性，而且 Transact\-SQL 指令碼無法在您指定的時間內執行，就會導致測試失敗。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[如何：建立空白 SQL Server 單元測試](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[如何：建立函式、觸發程序和預存程序的 SQL Server 單元測試](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[在 SQL Server 單元測試中使用測試條件](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)  
[解譯 SQL Server 單元測試結果](../ssdt/interpreting-sql-server-unit-test-results.md)  
[如何：執行 SQL Server 單元測試](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
