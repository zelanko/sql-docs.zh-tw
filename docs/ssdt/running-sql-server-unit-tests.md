---
title: 執行 SQL Server 單元測試
description: 了解 SQL Server 單元測試。 檢視有關建立測試、建立自訂測試條件、執行測試，以及解讀結果的資源。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconfig
ms.assetid: febcc87f-eb18-4c12-ba30-82ef0d49aaa3
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 810010b70a50f51c29b34b917af90127233d622c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987794"
---
# <a name="running-sql-server-unit-tests"></a>執行 SQL Server 單元測試

若要改善及維持程式碼的品質，您可以建立並執行 SQL Server 單元測試，該測試會驗證任何資料庫物件的行為，然後將這些測試簽入版本控制。 當您或小組的任何成員變更資料庫結構描述時，會同時執行 SQL Server 單元測試及軟體單元測試，以驗證該變更尚未中斷現有的功能。 您可以執行個別測試，或執行稱為測試清單的測試群組。 如需詳細資訊，請參閱[使用測試清單 (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/ms182461(v=vs.100))。  
  
## <a name="ways-to-run-sql-server-unit-tests"></a>執行 SQL Server 單元測試的方式  
您可以根據已安裝的軟體，透過幾種不同的方法執行 SQL Server 單元測試，如下所示：  
  
-   使用 Visual Studio 2010 中的 [測試檢視] 視窗執行測試。 如需詳細資訊，請參閱[如何：執行 SQL Server 單元測試](../ssdt/how-to-run-sql-server-unit-tests.md)及[如何：從 Microsoft Visual Studio 2010 執行自動化的測試](/previous-versions/visualstudio/visual-studio-2010/ms182470(v=vs.100))。 針對 Visual Studio 2012，請參閱[如何：從 Microsoft Visual Studio 2012 執行自動化的測試](/previous-versions/ms182470(v=vs.140))。  
  
-   在命令提示字元上使用 MSTest.exe 命令以執行測試。 如需詳細資訊，請參閱[如何：使用 MSTest 從命令列執行自動化測試 (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/ms182487(v=vs.100)) 或[如何：使用 MSTest 從命令列執行自動化測試 (Visual Studio 2012)](/previous-versions/ms182487(v=vs.140))。  
  
-   執行測試專案，從 [方案總管] 執行測試。 如需詳細資訊，請參閱[如何：從 Microsoft Visual Studio 2010 執行自動化測試](/previous-versions/visualstudio/visual-studio-2010/ms182470(v=vs.100))或[如何：從 Microsoft Visual Studio 2012 執行自動化測試](/previous-versions/ms182470(v=vs.140))。  
  
-   從 [測試結果] 視窗重新執行測試。 如需詳細資訊，請參閱[如何：重新執行測試 (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/ms182472(v=vs.100))。  
  
-   從 [測試清單編輯器] 視窗執行個別測試或測試清單 (Visual Studio 2010)。 如需詳細資訊，請參閱[如何：從 Microsoft Visual Studio 2010 執行自動化測試](/previous-versions/visualstudio/visual-studio-2010/ms182470(v=vs.100))或[如何：從 Microsoft Visual Studio 2012 執行自動化測試](/previous-versions/ms182470(v=vs.140))。  
  
-   在 Team Foundation Build 中建置專案時，執行測試。 如需詳細資訊，請參閱[如何：在建置應用程式之後設定和執行已排程的測試 (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/ms182465(v=vs.100)) 或[如何：在建置應用程式之後設定和執行已排程的測試 (Visual Studio 2012)](/previous-versions/visualstudio/visual-studio-2012/ms182465(v=vs.110))。  
  
您可以使用已排序的測試，按照特定的順序執行 SQL Server 單元測試。 如需詳細資訊，請參閱[如何：建立已排序的測試 (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/ms182631(v=vs.100)) 或[如何：建立已排序的測試 (Visual Studio 2012)](/previous-versions/ms182631(v=vs.140))。  
  
## <a name="interpreting-tests-results"></a>解譯測試結果  
執行測試後，[測試結果] 視窗中會顯示哪些測試成功，哪些失敗。 如需詳細資訊，請參閱[解譯 SQL Server 單元測試結果](../ssdt/interpreting-sql-server-unit-test-results.md)。 如需如何診斷未預期失敗的詳細資訊，請參閱[如何：針對資料庫物件進行偵錯](../ssdt/how-to-debug-database-objects.md)。  
  
## <a name="topics-in-this-section"></a>本節主題  
本節包含下列主題：  
  
-   [操作說明：針對資料庫物件進行偵錯](../ssdt/how-to-debug-database-objects.md)  
  
-   [操作說明：從 Team Foundation Build 執行 SQL Server 單元測試](../ssdt/how-to-run-sql-server-unit-tests-from-team-foundation-build.md)  
  
-   [操作說明：執行 SQL Server 單元測試](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
-   [解譯 SQL Server 單元測試結果](../ssdt/interpreting-sql-server-unit-test-results.md)  
  
## <a name="related-scenarios"></a>相關案例  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
您可以定義單元測試來驗證資料庫物件的行為，以及將每一個測試專案與不同的資料產生計劃、部署組態和連接字串產生關聯。  
  
[SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
您可以建立一個自訂的測試條件，來測試使用預設測試條件無法驗證的任何條件。  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
