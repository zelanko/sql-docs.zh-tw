---
title: 設定 SQL Server 單元測試執行
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: e0179429-13ce-4d23-ae27-e6419de0a575
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: d01703ff133fb8bac0425fc283190042d8dfcd1f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241571"
---
# <a name="how-to-configure-sql-server-unit-test-execution"></a>HOW TO：設定 SQL Server 單元測試執行

您可以藉由設定測試專案，指定可控制如何執行 SQL Server 單元測試的數個設定。 這些組態設定會儲存在測試專案的 app.config 檔案中。 如果直接編輯這個檔案，新的值會出現在測試組態對話方塊中。  
  
方案可以包含多個測試專案。 每個測試專案都會包含一個 app.config 檔案 (也就是一組組態設定)。 因此，方案可以包含幾組不同的單元測試 (每個測試專案各有一組)，設定以不同的方式執行。  
  
這些設定會控制您的測試如何連接到將要測試的資料庫、如何將結構描述從資料庫專案部署到該資料庫：  
  
-   **資料庫連接**： 使用這個設定，指定用來連接到要測試的資料庫之連接字串。 如需詳細資訊，請參閱[指定連接字串](#SpecifyConnectionStrings)  
  
-   **結構描述部署**： 「資料庫專案」(Database Project) 是資料庫的離線表示。 資料庫專案代表「資料庫物件」(Database Object) 的結構，但不包含資料。 當您在資料庫專案中變更「結構描述」(Schema) 之後，可以在實際資料庫中測試這些變更。 在結構描述部署步驟中，您要測試的資料庫物件會從資料庫專案複製到要執行測試的資料庫。 如需有關結構描述部署的詳細資訊，請參閱[部署資料庫結構描述](#DeployingDBSchema)。  
  
    > [!NOTE]  
    > 測試不會在方案資料夾中執行，而是在本機硬碟上的另一個資料夾中執行。 雖然您可以設定測試部署的各部分，但通常不需要針對單元測試設定部署。 如需有關測試部署的詳細資訊，請參閱[執行測試](https://msdn.microsoft.com/library/dd286680(VS.100).aspx)。  
  
## <a name="specify-connection-strings"></a><a name="SpecifyConnectionStrings"></a>指定連接字串  
  
#### <a name="to-specify-database-connection-strings"></a>若要指定資料庫連接字串  
  
1.  在 [方案總管]  中，以滑鼠右鍵按一下單元測試專案，然後按一下 [SQL Server 測試組態]  。  
  
    [SQL Server 測試組態 -' **']<projectname>** 對話方塊隨即出現。  
  
2.  在 [資料庫連接]  底下，您可以執行下列動作：  
  
    -   按一下要執行單元測試的資料庫連接。  
  
    -   如果您要對不同的資料庫連接驗證測試執行，選取 [使用次要資料連接來驗證單元測試]  核取方塊，然後按一下清單中的資料庫連接。  
  
    -   按一下 [新增連接]  ，將連接加入任一清單。 您也可以按一下 [編輯連接]  ，修改現有連接的設定。  
  
    這個步驟會建立 `ExecutionContext` 連接字串，用來執行單元測試中的測試指令碼。 如果您也指定了次要連接，也會建立 `PrivilegedContext` 連接字串。 這個連接會在單元測試的測試指令碼以外，測試與資料庫的互動。 如需詳細資訊，請參閱[連接字串和權限概觀](../ssdt/overview-of-connection-strings-and-permissions.md)。  
  
3.  按一下 [確定]  ，關閉 [SQL Server 測試組態 -' **']<projectname>** 對話方塊。  
  
4.  重建測試專案來套用組態變更。  
  
## <a name="deploy-a-database-schema"></a><a name="DeployingDBSchema"></a>部署資料庫結構描述  
  
#### <a name="to-deploy-to-a-database-the-schema-of-a-database-project"></a>若要將資料庫專案的結構描述部署到資料庫  
  
1.  在 [方案總管]  中，以滑鼠右鍵按一下資料庫專案，然後按一下 [建置]  。  
  
    當您建置資料庫專案時，會產生 Transact\-SQL 指令碼。 在對資料庫執行這個指令碼時，會在該資料庫中重新建立資料庫專案的結構。  
  
2.  選取要設定的測試專案。  
  
3.  在 [方案總管]  中，以滑鼠右鍵按一下單元測試專案，然後按一下 [SQL Server 測試組態]  。  
  
    [SQL Server 測試組態 -' **']<projectname>** 對話方塊隨即出現。  
  
4.  在 [部署]  底下，您可以執行下列動作：  
  
    -   選取 [執行測試前自動部署資料庫專案]  核取方塊，確定對資料庫專案所做的任何結構描述變更都會先認可，然後才執行測試。  
  
    -   在 [資料庫專案]  底下，按一下要部署的資料庫專案，或按一下省略符號以瀏覽其他專案。 資料庫專案檔的副檔名為 .dbproj。  
  
    -   在 [部署組態]  底下，按一下要部署的目標專案組態。 選項包括 [偵錯]  、[預設]  或 [發行]  。 不過，如果您建立單元測試的組態，該組態也會顯示為其中一個選項。  
  
5.  按一下 [確定]  ，關閉 [SQL Server 測試組態 -' **']<projectname>** 對話方塊。  
  
    在測試回合開始時，系統會執行步驟 1 中所產生的 Transact\-SQL 指令碼。 這個動作會將結構描述部署到目標資料庫。  
  
6.  重建單元測試專案來套用組態變更。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
