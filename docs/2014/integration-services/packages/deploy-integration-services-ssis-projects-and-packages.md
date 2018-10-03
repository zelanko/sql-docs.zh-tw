---
title: 部署專案和封裝 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9648e78567bbddf9209c53923cfe6c12d046d1a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200898"
---
# <a name="deployment-of-projects-and-packages"></a>部署專案和封裝
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援兩種部署模型：專案部署模型和封裝部署模型。 專案部署模型可讓您將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
 如需將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的詳細資訊，請參閱[將專案部署至 Integration Services 伺服器](../deploy-projects-to-integration-services-server.md)。  
  
 如需封裝部署模型的詳細資訊，請參閱[封裝部署&#40;SSIS&#41;](legacy-package-deployment-ssis.md)。  
  
## <a name="compare-project-deployment-and-package-deployment"></a>專案部署與封裝部署的比較  
 您為專案選擇的部署模型類型，會決定可用於該專案的開發及管理選項。 下表顯示使用專案部署模型與使用封裝部署模型之間的差異和相似性。  
  
|使用專案部署模型時|使用封裝部署模型時|  
|---------------------------------------------|---------------------------------------------|  
|專案是部署的單位。|封裝是部署的單位。|  
|參數可用來將值指派給封裝屬性。|組態可用來將值指派給封裝屬性。|  
|專案 (包含封裝和參數) 會建立至專案部署檔 (副檔名 .ispac)。|封裝 (副檔名 .dtsx) 和組態 (副檔名 .dtsconfig) 會個別儲存到檔案系統。|  
|專案 (包含封裝和參數) 部署到 SQL Server 執行個體上的 SSISDB 目錄。|封裝和組態會複製到另一台電腦上的檔案系統。 封裝也可以儲存至 SQL Server 執行個體上的 MSDB 資料庫。|  
|資料庫引擎上需要 CLR 整合。|資料庫引擎上不需要 CLR 整合。|  
|環境特定變數參數值會儲存在環境變數中。|環境特定組態值會儲存在組態檔中。|  
|在執行之前，可以先在伺服器上驗證目錄中的專案和封裝。 您可以使用 SQL Server Management Studio、預存程序或 Managed 程式碼來執行驗證。|臨執行前才驗證封裝。 您也可以用 dtExec 或 Managed 程式碼來驗證封裝。|  
|在資料庫引擎上啟動執行，藉以執行封裝。 在執行啟動之前，將專案識別碼、明確的參數值 (選擇性) 和環境參考 (選擇性) 指派給執行。<br /><br /> 您也可以使用 `dtExec` 執行封裝。|使用執行封裝`dtExec`和`DTExecUI`執行公用程式。 以命令提示字元引數 (選擇性) 來識別適用的組態。|  
|在執行期間，會自動擷取封裝所產生的事件，並儲存至目錄。 您可以用 Transact-SQL 檢視來查詢這些事件。|在執行期間，不會自動擷取封裝所產生的事件。 必須將記錄提供者加入封裝，才能擷取事件。|  
|封裝是在單獨的 Windows 處理序中執行。|封裝是在單獨的 Windows 處理序中執行。|  
|使用 SQL Server Agent 來排定封裝執行的時程。|使用 SQL Server Agent 來排定封裝執行的時程。|  
  
## <a name="features-of-project-deployment-model"></a>專案部署模型的功能  
 下表列出可用於專為專案部署模型開發之專案的功能。  
  
|功能|描述|  
|-------------|-----------------|  
|參數|參數指定要供封裝使用的資料。 您可以將參數範圍限定在分別具有封裝參數和專案參數的封裝層級或專案層級。 在運算式或工作中，都會用到參數。 將專案部署到目錄之後，您可以為每個參數各指定一個常值，或是使用在設計時所指派的預設值。 您也可以參考環境變數來替代常值。 環境變數會在封裝執行時解析。|  
|環境|環境是可供 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案參考之變數的容器。 每個專案都可以有多個環境參考，但是封裝執行的單一執行個體只能參考來自單一環境的變數。 環境可讓您組織指派給封裝的值。 例如，您可能會有命名為 "Dev"、"test" 和 "Production" 的環境。|  
|環境變數|環境變數定義在封裝執行期間，可指派給參數的常值。 若要使用環境變數，請建立環境參考 (在對應至具有參數之環境的專案中)、指派參數值給環境變數的名稱，並且在設定執行的執行個體時，指定相對應的環境參考。|  
|SSISDB 目錄|所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件都會在名為 SSISDB 目錄之資料庫中的 SQL Server 執行個體上儲存及管理。 該目錄可讓您使用資料夾專案和環境。 SQL Server 的每個執行個體都可以有一個目錄。 每個目錄中可以有零個或多個資料夾。 每個資料夾可以有零個以上的專案和零個以上的環境。 目錄中的資料夾也可以用作對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件的權限界限。|  
|目錄預存程序和檢視|有大量的預存程序和檢視可用來管理目錄中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件。 例如，您可以指定參數和環境變數的值、建立和啟動執行，以及監視目錄作業。 您甚至可以在執行啟動之前，查看封裝將要使用哪些確切的值。|  
  
## <a name="project-deployment"></a>專案部署  
 專案部署模型的中心是專案部署檔案 (副檔名 .ispac)。 專案部署檔案是獨立的 (self-contained) 部署單位，其中只包含專案中封裝和參數的相關基本資訊。 專案部署檔案不會擷取 Integration Services 專案檔 (副檔名 .dtproj) 中包含的所有資訊。 例如，您用來撰寫附註的其他文字檔不是儲存在專案部署檔案中，因此不會部署至目錄。  
  
## <a name="required-tasks"></a>必要的工作  
  
-   [將專案部署至 Integration Services 伺服器](../deploy-projects-to-integration-services-server.md)  
  
## <a name="related-content"></a>相關內容  
 mattmasson.com 上的部落格文章： [Thoughts on Branching Strategies for SSIS Projects](http://go.microsoft.com/fwlink/?LinkId=245739)。  
  
## <a name="see-also"></a>另請參閱  
 [dtexec 公用程式](dtexec-utility.md)  
  
  
