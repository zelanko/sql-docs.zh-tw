---
title: 如何：建立 SQL Server 資料庫單元測試的測試專案 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b3e7ba8-b565-4689-af1a-34cc255b7c60
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f641380e18dbcb042e36704627e1e39e2f9a4e7
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563645"
---
# <a name="how-to-create-a-test-project-for-sql-server-database-unit-testing"></a>HOW TO：建立 SQL Server 資料庫單元測試的測試專案
在您開始撰寫評估資料庫物件的單元測試之前，必須先建立測試專案。 這個專案會包含 SQL Server 單元測試，但是它可以包含其他類型的測試。  
  
您可以將給定資料庫專案的所有 SQL Server 單元測試都放在單一測試專案內。 不過，您可能會想要根據下列問題的回答，建立其他測試專案：  
  
|||  
|-|-|  
|**問題**|**決策**|  
|不同的 SQL Server 單元測試是否需要針對測試執行或測試驗證存取不同的資料庫連接？|如果是，您就需要多個測試專案。 您無法針對測試執行指定多個資料庫連接。 不過，您可以針對測試驗證指定不同的資料庫連接。|  
|您是否想要針對不同的單元測試部署不同的資料庫專案？|如果是，您就需要多個測試專案。 測試專案只能部署單一資料庫專案。|  
  
如需其中一個問題的詳細資訊，請參閱[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)。 您也可以提供自己的 [DatabaseTestService](https://msdn.microsoft.com/library/microsoft.data.schema.unittesting.databasetestservice.aspx) Microsoft.Data.Schema.UnitTesting.DatabaseTestService 實作，作為建立多個測試專案的替代方案。  
  
您有三個選項可以將測試專案加入至包含資料庫專案的方案：  
  
-   將測試專案加入至方案。 測試專案包含您可以刪除的標準單元測試。 這個專案不包含您必須加入的 SQL Server 單元測試類別。  
  
-   從 [測試] 功能表加入新的 SQL Server 單元測試。 當您加入單元測試時，SQL Server Data Tools 也會建立測試專案 (如果您要求的話)。 此專案包含 SQL Server 單元測試類別。 SQL Server 單元測試測試類別包含一個或多個單元測試。  
  
-   從 SQL Server [物件總管] 中開啟的專案中，從預存程序、函式或觸發程序建立單元測試。 當您建立單元測試時，SQL Server Data Tools 也會建立測試專案 (如果您要求的話)。 此專案包含 SQL Server 單元測試類別。 SQL Server 測試類別包含一個或多個單元測試。  
  
下列程序將概述每種方法。  
  
### <a name="to-add-a-test-project-to-an-existing-solution"></a>若要將測試專案加入至現有的方案  
  
1.  在 [ **檔案** ] 功能表中，指向 [ **新增**]，然後按一下 [ **專案**]。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在 [已安裝的範本] 底下，展開 [SQL Server] 節點，然後選取 [SQL Server 資料庫專案]。  
  
3.  在 [名稱] 中，輸入專案名稱。  
  
### <a name="to-create-a-test-project-with-a-sql-server-unit-test-class"></a>若要建立包含 SQL Server 單元測試類別的測試專案  
  
-   請依照[如何：建立空白 SQL Server 單元測試](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)或[如何：建立函式、觸發程序和預存程序的 SQL Server 單元測試](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)中所述的程序進行。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
