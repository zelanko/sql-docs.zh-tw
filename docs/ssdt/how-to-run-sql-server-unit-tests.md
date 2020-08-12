---
title: 執行 SQL Server 單元測試
description: 了解如何執行 SQL Server 單元測試。 了解在不同版本的 Visual Studio 中，從各種視窗和工具執行測試的步驟。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ed1a61d719063643d0fef3c1c0598e45cec54555
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893878"
---
# <a name="how-to-run-sql-server-unit-tests"></a>如何：執行 SQL Server 單元測試

您可以使用數種方式的任何一種來執行 SQL Server 單元測試，例如使用各種視窗和 [命令提示字元] 視窗。  
  
> [!NOTE]  
> 您不可以從遠端執行單元測試。  
  
可用的方式取決於您所安裝的軟體，如[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)中所述。  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>若要使用測試檢視 (Visual Studio 2010) 執行 SQL Server 單元測試  
  
1.  在 [測試] 功能表上，指向 [Windows]，然後按一下 [測試檢視]。  
  
    [測試檢視] 視窗隨即開啟。  
  
2.  在 [測試檢視] 視窗中，按一下您想要執行的一個或多個測試。 您可以使用 CTRL 鍵或 SHIFT 鍵來指定不連續或連續的測試區塊。  
  
3.  執行下列任一步驟：  
  
    -   以滑鼠右鍵按一下 [測試檢視] 視窗的介面，然後按一下 [執行選取範圍]。  
  
    -   在 [測試檢視] 工具列上，按一下 [執行選取範圍]。  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>若要使用測試總管 (Visual Studio 2012) 執行 SQL Server 單元測試  
  
1.  在 [測試] 功能表上，指向 [Windows]，然後按一下 [測試總管]。  
  
    [測試總管] 視窗隨即開啟。  
  
2.  在 [測試總管] 中，按一下您想要執行的一個或多個測試。 您可以使用 CTRL 鍵或 SHIFT 鍵來指定不連續或連續的測試區塊。  
  
3.  以滑鼠右鍵按一下其中一個反白顯示的測試，然後按一下 [執行選取的測試]。  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>若要從 SQL Server 單元測試設計工具 (Visual Studio 2010) 執行 SQL Server 單元測試  
  
-   在 [測試工具] 工具列上，您會找到使用或不使用偵錯工具啟動專案的按鈕。  
  
這個步驟會在目前的測試回合中執行所有測試。 啟動測試回合之後，[測試結果] 視窗隨即出現並顯示測試回合的進度。 這個顯示畫面包括執行中的測試以及已完成的測試。 如需詳細資訊，請參閱[解譯 SQL Server 單元測試結果](../ssdt/interpreting-sql-server-unit-test-results.md)。  
  
## <a name="see-also"></a>另請參閱  
[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)  
[操作說明：從 Microsoft Visual Studio 2010 執行自動化的測試](https://msdn.microsoft.com/library/ms182470(VS.100).aspx)  
[從命令列執行自動化測試 (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182486(VS.100).aspx)  
[測試應用程式 (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182409.aspx)  
  
