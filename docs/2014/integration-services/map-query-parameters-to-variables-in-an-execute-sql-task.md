---
title: 將查詢參數對應至變數，在執行 SQL 工作 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameterized SQL commands [Integration Services]
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- Execute SQL task [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 6a164349-dfcf-4995-80bc-d4e7aee52a83
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b0f1add0f2d249922f00fc1b16d5da12bb903faf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524992"
---
# <a name="map-query-parameters-to-variables-in-an-execute-sql-task"></a>在執行 SQL 工作中將查詢參數對應到變數
  此主題描述如何在「執行 SQL」工作中使用參數化 SQL 陳述式，以及建立 SQL 陳述式中變數和參數之間的對應。  
  
 若要深入了解如何搭配不同連接類型使用的執行 SQL 工作、參數標記和參數名稱，請參閱 [執行 SQL 工作](control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>將查詢參數對應至變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟您要使用的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  如果封裝尚未包含執行 SQL 工作，則會加入一個執行 SQL 工作至封裝的控制流程。 如需詳細資訊，請參閱[加入或刪除工作或容器中的控制流程](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  按兩下執行 SQL 工作。  
  
6.  以下列方式的其中之一提供參數化 SQL 命令：  
  
    -   使用直接輸入，並在 SQLStatement 屬性中輸入 SQL 命令。  
  
    -   使用直接輸入，按一下 [建立查詢]，然後使用「查詢產生器」提供的圖形工具來建立 SQL 命令。  
  
    -   使用檔案連接，然後參考包含 SQL 命令的檔案。  
  
    -   使用變數，然後參考包含 SQL 命令的變數。  
  
     您在參數化 SQL 陳述式中使用的參數標記，需視「執行 SQL」工作所使用的連接類型而定。  
  
    |連接類型|參數標記|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET 和 SQLMOBILE|@\<參數名稱>|  
    |ODBC|?|  
    |EXCEL 和 OLE DB|?|  
  
     下表依照連接管理員類型列出 SELECT 命令的範例。 參數會在 WHERE 子句中提供篩選值。 這些範例使用 SELECT，從 **中的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 資料表傳回 **ProductID** 大於及小於兩個參數所指定之值的產品。  
  
    |連接類型|SELECT 語法|  
    |---------------------|-------------------|  
    |EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
     如需使用參數搭配預存程序的範例，請參閱[執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
7.  按一下 [參數對應]。  
  
8.  若要加入參數對應，請按一下 [加入]。  
  
9. 在 [參數名稱] 方塊中提供名稱。  
  
     您所使用的參數名稱需視「執行 SQL」工作所使用的連接類型而定。  
  
    |連接類型|參數名稱|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, ...|  
    |ADO.NET 和 SQLMOBILE|@\<參數名稱>|  
    |ODBC|1, 2, 3, ...|  
    |EXCEL 和 OLE DB|0, 1, 2, 3, ...|  
  
10. 從 [變數名稱] 清單中，選取一個變數。 如需詳細資訊，請參閱[加入、刪除、變更封裝中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)。  
  
11. 在 [方向] 清單中，指定參數是輸入、輸出還是傳回值。  
  
12. 在 [資料類型] 清單中，設定參數的資料類型。  
  
    > [!IMPORTANT]  
    >  參數的資料類型必須與變數的資料類型相容。  
  
13. 針對 SQL 陳述式中的每個參數，重複步驟 8 到 11。  
  
    > [!IMPORTANT]  
    >  參數對應的順序必須與參數在 SQL 陳述式中出現的順序相同。  
  
14. 按一下 [確定] 。  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL 工作](control-flow/execute-sql-task.md)   
 [參數和傳回碼中執行 SQL 工作](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)   
 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)  
  
  
