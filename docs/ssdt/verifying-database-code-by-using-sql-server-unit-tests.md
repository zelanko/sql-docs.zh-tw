---
title: 使用 SQL Server 單元測試驗證資料庫程式碼
description: 了解 SQL Server 單元測試。 查看哪些 Visual Studio 版本提供對測試的支援，以及檢視有關使用測試來確認資料庫程式碼的資源。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 003713e2-de6b-4277-a0a8-7d1f2f4ffb39
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ac5f8d848e2bc6591b0065e21c7588e4977c0d73
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987734"
---
# <a name="verifying-database-code-by-using-sql-server-unit-tests"></a>使用 SQL Server 單元測試驗證資料庫程式碼

您可以使用 SQL Server 單元測試建立資料庫的基準狀態，然後驗證您對資料庫物件所做的任何後續變更。  
  
若要建立資料庫的基準狀態，您可以建立測試專案，並撰寫可對資料庫物件進行操作的 Transact\-SQL 集。 藉由使用這些測試，您可以在隔離的開發環境中驗證那些物件功能是否為預期的功能。 SQL Server 單元測試非常適合使用 SQL Server 資料庫專案結合離線資料庫開發一起運作 (如需詳細資訊，請參閱[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md))。 有了 SQL Server 單元測試的基準集之後，您就可以使用這些測試，驗證資料庫是否正確運作，然後再將變更簽入至版本控制。  
  
您可以建立測試來驗證任何資料庫物件的變更。 此外，您還可以自動產生測試資料庫函式、觸發程序和預存程序的 Transact\-SQL 程式碼虛設常式。  
  
> [!NOTE]  
> 您可以在不開啟資料庫專案的情況下，建立並執行 SQL Server 單元測試。 不過，如果您想要自動產生測試指令碼來測試專案中的特定資料庫物件，就必須開啟包含您想要測試之物件的資料庫專案。  
  
當您或您的小組成員變更資料庫結構描述時，您可以使用這些測試來驗證變更是否中斷了現有的功能。 您可以建立 SQL Server 單元測試來補充軟體開發人員所建立的軟體單元測試。 您必須完成這兩個測試集以驗證應用程式的整體行為。  
  
當程序必須成功時，您的單元測試可以驗證程序是否成功；當程序必須失敗時，則可驗證程序是否失敗。 測試適當的失敗是否發生稱為負面測試。  
  
## <a name="visual-studio-editions-support-for-sql-server-unit-tests"></a>Visual Studio 各版本對 SQL Server 單元測試的支援  
已在 SQL Server Data Tools 的 2012 年 12 月更新中新增的 SQL Server 單元測試功能，可讓您在 Visual Studio 2010 Professional 和 Visual Studio 2012 Professional 及更新版本中，建立、修改及執行 SQL Server 單元測試。  
  
為確保您安裝的是最新的 SQL Server Data Tools 更新，請存取 [[檢查更新] 對話方塊](../ssdt/check-for-updates-dialog-box.md)。  
  
Visual Studio 2010 和 Visual Studio 2012 整合的 SQL Server Data Tools 殼層不支援 SQL Server 單元測試。  
  
## <a name="common-tasks"></a>一般工作  
下表列出支援此案例之一般工作的說明，以及詳細資訊的連結，這些資訊可幫助您成功完成這些工作。  
  
|一般工作|支援內容|  
|----------------|----------------------|  
|**進行實作練習：** 您可以遵循入門逐步解說來熟悉如何建立並執行簡單的 SQL Server 單元測試。 這個逐步解說包含了負面 SQL Server 單元測試的範例。|[逐步解說：建立及執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**定義 SQL Server 單元測試：** 您必須在其自身的專案中建立 SQL Server 單元測試。 您可以針對該專案進行設定，並且針對每個測試定義一個或多個測試條件。|[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)<br /><br />[在 SQL Server 單元測試中使用測試條件](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)|  
|**執行 SQL Server 單元測試**：定義一或多個單元測試之後，您就可以執行這些單元測試、針對任何問題進行偵錯，以及檢查測試結果。|[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)|  
|**管理測試群組 (Visual Studio 2010)：** 若它們通常會在相同的時間執行，您可以將測試組織成群組。 雖然系統仍然支援測試清單，不過您應該針對新的測試群組考慮改用測試分類。 例如，您可能會針對觸發程序或特定*結構描述*中的所有物件測試，建立測試分類。|[定義測試分類以將測試分組](/previous-versions/visualstudio/visual-studio-2010/dd286595(v=vs.100))<br /><br />[定義測試清單以將測試分組](/previous-versions/visualstudio/visual-studio-2010/dd286584(v=vs.100))|  
|**將您的測試專案和測試簽入至版本控制**：在您執行測試並驗證測試是否正確運作之後，應該將測試專案及所有相關聯的檔案簽入至版本控制，讓所有小組成員都能夠執行您的測試。 您可以透過將測試專案與 SQL Server 資料庫專案簽入版本控制，輕鬆還原資料庫和資料庫測試的相容版本。|[將檔案加入至版本控制](/previous-versions/visualstudio/visual-studio-2010/ms181374(v=vs.100))<br /><br />[使用簽入和暫止的變更視窗](/previous-versions/visualstudio/visual-studio-2010/ms245462(v=vs.100)) \(機器翻譯\)|  
|**定義自訂測試條件**：如果您必須測試預設測試條件集不包含的行為，可以建立自訂測試條件。 您必須將這些條件散發給所有想要執行使用新條件之測試的小組成員。|[案例：為 SQL Server 單元測試定義自訂測試條件](/previous-versions/visualstudio/visual-studio-2010/dd193282(v=vs.100))|  
|**更新現有的單元測試**：如果您擁有在舊版 Visual Studio 中建立的資料庫單元測試，必須先升級這些測試，才能順利使用這個版本建置並執行測試。<br /><br />**注意**：如果您所開啟的方案同時包含來自舊版 Visual Studio 的資料庫專案和資料庫單元測試專案，系統會提示您升級資料庫專案。 系統不會提示您升級資料庫單元測試專案，您必須將它手動升級。|[升級包含資料庫單元測試的舊版測試專案](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)|  
|**擴充性：** 您可以建立延伸模組來延伸 SQL Server Data Tools。|[SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)|  
|**針對問題進行疑難排解：** 您可以深入了解如何針對常見 SQL Server 單元測試問題進行疑難排解。|[針對 SQL Server 資料庫單元測試問題進行疑難排解](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>相關案例  
[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)  
搭配使用 SQL Server 資料庫專案的離線專案開發時，資料庫單元測試特別有效。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
