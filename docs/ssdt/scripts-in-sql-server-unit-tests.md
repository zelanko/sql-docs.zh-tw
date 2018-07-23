---
title: SQL Server 單元測試中的指令碼 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80c5cf62-a9c9-4e9d-8c6f-8eed50a595a7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f829c583b0591263eeb5db612983efc18e96fa97
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085880"
---
# <a name="scripts-in-sql-server-unit-tests"></a>SQL Server 單元測試中的指令碼
每個 SQL Server 單元測試都包含單一測試前動作、測試動作和測試後動作。 其中每個動作又包含下列項目：  
  
-   在資料庫上執行的 Transact\-SQL 指令碼。  
  
-   零或多個評估指令碼執行所傳回之結果的測試條件。  
  
測試動作中的 Transact\-SQL 測試指令碼是您必須包含在每個 SQL Server 單元測試中的唯一元件。 除了測試指令碼本身以外，您可能也會想要指定測試條件以驗證測試指令碼是否傳回您所預期的值或一組值。 測試動作會演練或變更該資料庫中的特定物件，然後評估該變更。  
  
您可以針對每個測試動作包含一個測試前動作和一個測試後動作。 與測試動作相似之處在於，每個測試前動作和每個測試後動作都包含一個 Transact\-SQL 指令碼以及零或多個測試條件。 您可以使用測試前動作來確保資料庫所處的狀態可讓測試動作執行並傳回有意義的結果。 例如，您可以使用測試前動作來驗證資料表是否包含資料，然後測試指令碼再針對該項資料執行作業。 在測試前動作備妥資料庫，而且測試動作傳回有意義的結果之後，測試後動作可用來讓資料庫返回執行測試前動作之前所處的狀態。 或在某些情況下，您可能會使用測試後動作來驗證測試動作的結果。 這是因為測試後動作可能會比測試動作擁有更高的資料庫權限。 如需詳細資訊，請參閱[連接字串和權限概觀](../ssdt/overview-of-connection-strings-and-permissions.md)。  
  
除了這三個動作之外，還有兩個在每個 SQL Server 單元測試執行前後執行的測試指令碼 (稱為通用指令碼)。 因此，您最多可以在單一 SQL Server 單元測試執行期間執行五個 Transact\-SQL 指令碼。 只有測試動作所包含的 Transact\-SQL 指令碼是必要項；通用指令碼以及測試前和測試後動作指令碼是選擇項。  
  
下表將提供與任何 SQL Server 單元測試相關聯之指令碼的完整清單。  
  
|**動作**|**指令碼類型**|**說明**|  
|--------------|-------------------|-------------------|  
|TestInitialize|通用指令碼 (初始化)|(選擇項) 這個指令碼優先於單元測試中的所有測試前和測試動作。 TestInitialize 指令碼會在給定測試類別中的每個單元測試之前執行。 這個指令碼會使用授權的內容來執行。|  
|測試前|測試指令碼|(選擇項) 這個指令碼屬於單元測試的一部分。 測試前指令碼會在單元測試中的測試動作之前執行。 這個指令碼會使用授權的內容來執行。|  
|測試|測試指令碼|(必要項) 這個指令碼屬於單元測試的一部分。 例如，這個指令碼可能會執行取得、插入或更新資料表值的預存程序。 這個指令碼會使用執行內容來執行。|  
|測試後|測試指令碼|(選擇項) 這個指令碼屬於單元測試的一部分。 測試後指令碼會在個別的單元測試之後執行。 這個指令碼會使用授權的內容來執行。|  
|TestCleanup|通用指令碼 (清除)|(選擇項) 這個指令碼是接在單元測試後面。 TestCleanup 指令碼會在給定測試類別中的所有單元測試之後執行。 這個指令碼會使用授權的內容來執行。|  
  
如需有關執行每個指令碼所在不同安全性內容的詳細資訊，請參閱[連接字串和權限概觀](../ssdt/overview-of-connection-strings-and-permissions.md)以及 [SQL Server Data Tools 的必要權限](../ssdt/required-permissions-for-sql-server-data-tools.md)中的＜SQL Server 單元測試權限＞一節。  
  
## <a name="order-in-which-scripts-are-run"></a>指令碼的執行順序  
請務必了解每個指令碼的執行順序。 雖然您無法變更該順序，不過可以決定想要執行的指令碼。 下圖包含您可以在含有兩個 SQL Server 單元測試之測試回合中使用的指令碼選項，並且顯示這些指令碼的執行順序：  
  
![兩個資料庫單元測試](../ssdt/media/twodatabaseunittests.png "兩個資料庫單元測試")  
  
> [!NOTE]  
> 如果已設定 SQL Server 資料庫專案部署，這會出現在測試回合開始時授權的內容連接字串底下。 如需詳細資訊，請參閱[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)。  
  
## <a name="initialization-and-cleanup-scripts"></a>初始化和清除指令碼  
在 SQL Server 單元測試設計工具中，TestInitialize 和 TestCleanup 指令碼稱為通用指令碼。 先前的範例是假設兩個單元測試都屬於相同測試類別的一部分。 因此，它們會共用相同的 TestInitialize 和 TestCleanup 指令碼。 對於單一測試類別內的所有單元測試而言，一律是如此。 不過，如果您的測試回合包含不同測試類別的單元測試，相關聯測試類別的通用指令碼將會在單元測試執行前後執行。  
  
如果您只有使用 SQL Server 單元測試設計工具撰寫單元測試，可能會不熟悉測試類別的概念。 每當您透過開啟 [測試] 功能表並按一下 [新增測試] 來建立單元測試時，SQL Server Data Tools 都會產生測試類別。 出現在 [方案總管] 中的測試類別會使用您所指定的測試名稱，後面接著 .cs 或 .vb 副檔名。 在每個測試類別中，個別的單元測試會儲存成測試方法。 不過，不論測試方法 (即單元測試) 的數目為何，每個測試類別都可以有零或一個 TestInitialize 和 TestCleanup 指令碼。  
  
您可以使用 TestInitialize 指令碼來準備測試資料庫，而且可以使用 TestCleanup 指令碼，讓測試資料庫返回已知狀態。 例如，您可以先使用 TestInitialize 來建立協助程式預存程序，之後在測試指令碼中執行該預存程序以測試不同的預存程序。  
  
## <a name="pre-test-and-post-test-scripts"></a>測試前和測試後指令碼  
與測試前和測試後動作相關聯的指令碼可能會因單元測試而異。 您可以使用這些指令碼來建立資料庫的累加變更，然後再清除這些變更。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[在 SQL Server 單元測試中使用測試條件](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
  
