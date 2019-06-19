---
title: 如何：建立空白 SQL Server 單元測試 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.createtest
ms.assetid: b6f3cd5a-3389-42d6-a93f-97b3ddf31b95
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8921129e8e5b7afcf3f141749bc31ec857a166e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098033"
---
# <a name="how-to-create-an-empty-sql-server-unit-test"></a>如何：建立空白 SQL Server 單元測試
將單元測試包含在資料庫專案中來驗證您對資料庫物件所做的變更，並不會中斷現有的功能。 下列程序說明如何為任何資料庫物件建立 SQL Server 單元測試。 SQL Server Data Tools 包括一些對資料庫函數、觸發程序和預存程序的額外支援。 如需詳細資訊，請參閱[如何：建立函式、觸發程序和預存程序的 SQL Server 單元測試](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)。  
  
當您使用第一個程序建立 SQL Server 單元測試時，如果沒有測試專案存在，則會自動為您建立一個測試專案。 如果測試專案已經存在，您可以選擇將新的測試加入到其中一個專案，也可以建立新的測試專案。 如需測試專案的詳細資訊，請參閱[如何：建立 SQL Server 資料庫單元測試的測試專案](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)。  
  
在建立 SQL Server 單元測試時，您有兩個選擇：  
  
-   在新的測試類別內建立新的 SQL Server 單元測試。  
  
    所指定測試類別內的所有 SQL Server 單元測試都將使用相同的 TestInitialize 和 TestCleanup 指令碼。 如果您希望您的單元測試使用與其他單元測試不同的 TestInitialize 和 TestCleanup 指令碼，請建立新的測試類別。 如需詳細資訊，請參閱 [SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)。  
  
-   在現有的測試類別內建立新的 SQL Server 單元測試。  
  
    如果您希望您的單元測試使用與此類別內其他單元測試相同的 TestInitialize 和 TestCleanup 指令碼，請選擇這個選項。  
  
### <a name="to-create-a-sql-server-unit-test-inside-a-new-test-class"></a>在新的測試類別內建立 SQL Server 單元測試  
  
1.  在 [測試] 功能表上，按一下 [新增測試]。  
  
    [加入新測試] 對話方塊隨即出現。  
  
2.  在 [範本] 底下，按一下 [SQL Server 單元測試]。  
  
3.  在 [測試名稱] 底下，輸入測試名稱。  
  
4.  在 [加入至測試專案] 底下，選取要將這個測試加入其中的現有測試專案。 如果沒有任何測試專案存在，或是您想要建立新的測試專案，請選取 [建立新的 <language> 測試專案]。  
  
5.  按一下 [確定] 。  
  
    如果您的測試專案是新的，則會出現 [新增測試專案] 對話方塊。 為專案命名，然後按一下 [確定]。  
  
    如果您的測試專案是新的或尚未設定，則會出現 [SQL Server 測試組態 <ProjectName>] 對話方塊。 這個對話方塊可讓您針對測試專案設定以下資訊：  
  
    -   用來執行測試的資料庫連接。  
  
    -   用來驗證測試結果、部署資料庫及產生資料的資料庫連接。  
  
    -   在您執行單元測試之前，資料庫專案與給定專案組態的任何相關結構描述變更之自動部署。  
  
    如需詳細資訊，請參閱[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)。  
  
6.  提供專案組態資訊，然後按一下 [確定]。  
  
    \- 或 -  
  
    按一下 [取消] 即可建立單元測試，而不設定測試專案。  
  
    您的空白測試會出現在 [SQL Server 單元測試設計工具] 中。 視您為建立測試專案指定的語言而定，會在測試專案中加入 Visual Basic 或 Visual C\# 原始程式碼檔。 這個檔案包含 SQL Server Data Tools 針對您剛才建立之單元測試所產生的 SQL Server 單元測試類別。 這個測試類別可包含一或多個單元測試，您可以透過 [SQL Server 單元測試設計工具] 或是透過測試類別中當成新測試方法的程式碼，加入這些單元測試。  
  
    您也可以透過下列方式加入其他測試：  
  
    -   在 [方案總管] 中以滑鼠右鍵按一下測試專案，依序選取 [加入]、[新增測試] 和 [SQL Server 單元測試]。  
  
    -   在 SQL Server 的 [物件總管] 中，選取 [建立單元測試]。  
  
    當您在 [方案總管] 中選取這個檔案時，此檔案預設會顯示在 [SQL Server 單元測試設計工具] 中。 若要檢視程式碼或自訂程式碼，以便在單元測試中加入更多的功能，請選取這個檔案，然後按一下滑鼠右鍵，再選擇 [檢視程式碼]。  
  
### <a name="to-create-a-sql-server-unit-test-inside-an-existing-test-class"></a>在現有的測試類別內建立 SQL Server 單元測試  
  
1.  在 [SQL Server 單元測試設計工具] 中開啟現有的 SQL Server 單元測試類別。 您可以在 [方案總管] 中按兩下單元測試原始程式碼檔，以存取 [SQL Server 單元測試設計工具]。  
  
2.  按一下巡覽列中的加號 (**+**)，以顯示 [指定單元測試名稱] 對話方塊。  
  
3.  輸入名稱，然後按一下 [確定]。  
  
    新的 SQL Server 單元測試就會出現在巡覽列的下拉式清單中， 它也會以測試類別中的新測試方法形式加入。 若要在程式碼中檢視此測試方法，請選取類別檔案，然後按一下滑鼠右鍵，再選擇 [檢視程式碼]。 目前的測試類別檔案名稱會顯示在 [SQL Server 單元測試設計工具] 最上方的索引標籤上。  
  
在您設定測試專案並建立單元測試之後，後續的步驟如下：  
  
-   加入 Transact\-SQL 測試指令碼。  
  
-   定義測試前和測試後動作。  
  
-   加入測試條件或其他判斷提示陳述式來驗證指令碼的結果。  
  
> [!NOTE]  
> 結果不明的測試條件是加入到每一個測試中的預設條件。 包含這個測試條件的目的為要指出尚未實作測試驗證。 當您已經加入其他測試條件之後，請從測試中刪除這個測試條件。 如需詳細資訊，請參閱[如何：將測試條件新增至資料庫單元測試](https://msdn.microsoft.com/library/aa833242(VS.100).aspx)。  
  
## <a name="see-also"></a>另請參閱  
[操作說明：執行 SQL Server 單元測試](../ssdt/how-to-run-sql-server-unit-tests.md)  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[建立單元測試](https://msdn.microsoft.com/library/ms182523(VS.90).aspx)  
  
