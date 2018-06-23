---
title: 結果集對應至變數，在執行 SQL 工作 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 62dab9509a080e00edc4d990cd3f23fa67c93113
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146330"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>在執行 SQL 工作中將結果集對應至變數
  此主題描述如何在執行 SQL 工作中，建立結果集與變數之間的對應。 將結果集對應至變數後，封裝中的其他元素便可使用該結果集。 例如，指令碼工作中的指令碼可以讀取變數，然後使用結果集中的值，或是 XML 來源可以使用儲存在變數中的結果集。 如果結果集由父封裝產生，則可以藉由將結果集對應至父封裝中的變數，然後在子封裝中建立用來儲存父變數值的父封裝變數組態，以便讓「執行封裝」工作所呼叫的子封裝可以使用結果集。  
  
 如需不同類型結果集以及您可以對應至結果集之變數資料類型的描述，請參閱 [執行 SQL 工作中的結果集](control-flow/execute-sql-task.md)。  
  
### <a name="to-map-a-result-set-to-a-variable"></a>將結果集對應至變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  如果封裝尚未包含執行 SQL 工作，則會加入一個執行 SQL 工作至封裝的控制流程。 如需詳細資訊，請參閱[加入或刪除工作或容器中的控制流程](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  執行個體時提供 SQL Server 登入。  
  
5.  按兩下執行 SQL 工作。  
  
6.  在 [執行 SQL 工作編輯器] 對話方塊的 [一般] 頁面上，選取 [單一資料列]、[完整結果集] 或 [XML] 結果集類型。  
  
     如需不同結果集的描述，請參閱[執行 SQL 工作中的結果集](result-sets-in-the-execute-sql-task.md)  
  
7.  按一下 [結果集]。  
  
8.  若要加入結果集對應，請按一下 [加入]。  
  
9. 從 [變數名稱] 清單中，選取變數或新建變數。 如需詳細資訊，請參閱[加入、刪除、變更封裝中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)。  
  
     如需可對應至不同結果集之變數資料類型的描述，請參閱 [執行 SQL 工作中的結果集](result-sets-in-the-execute-sql-task.md)。  
  
     如需如何將變數對應至單一資料行以及將多個變數對應至多個資料行的相關資訊，請參閱[執行 SQL 工作中的結果集](control-flow/execute-sql-task.md)中的**以結果集填入變數**一節。  
  
10. 在 [結果名稱] 清單中，選擇性地修改結果集的名稱。  
  
     一般而言，您可以使用資料行名稱做為結果集名稱，也可以資料行清單中資料行的序數位置做為結果集。 使用資料行名稱做為結果集名稱的功能取決於將該工作設定為使用的提供者。 並非所有的提供者可以使用資料行名稱做為結果集名稱。  
  
11. 按一下 [確定] 。  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL 工作](control-flow/execute-sql-task.md)   
 [中的結果集執行 SQL 工作](result-sets-in-the-execute-sql-task.md)   
 [執行封裝工作](control-flow/execute-package-task.md)   
 [封裝組態](../../2014/integration-services/package-configurations.md)   
 [建立封裝組態](../../2014/integration-services/create-package-configurations.md)   
 [子封裝中使用變數和參數的值](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Integration Services &#40;SSIS&#41;變數](integration-services-ssis-variables.md)  
  
  