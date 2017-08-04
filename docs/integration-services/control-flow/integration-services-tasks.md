---
title: "Integration Services 工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Integration Services], tasks
- files [Integration Services], task options
- workflow tasks [Integration Services]
- Integration Services, tasks
- adding package tasks
- tasks [Integration Services], listed
- SSIS tasks
- SSIS, tasks
- control flow [Integration Services], tasks
- tasks [Integration Services]
- grouping tasks
- tasks [Integration Services], about tasks
- SQL Server Integration Services tasks
- data preparation tasks [Integration Services]
- directory operations [Integration Services]
ms.assetid: 75c8901d-6966-4af3-abe5-10af6dd9313b
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 00504d62d603f43b567394180b9e03dee34a1ed7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-tasks"></a>Integration Services 工作
  工作為控制流程元素，用來定義封裝控制流程中所執行工作的單位。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝是由一或多項工作所組成。 如果封裝包含超過一項工作，則會在控制流程中按照優先順序條件約束連接並排列順序。  
  
 您也可以使用支援 COM 的程式設計語言 (例如 Visual Basic) 或 .NET 程式設計語言 (例如 C#) 撰寫自訂工作。  
  
 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中使用封裝的圖形工具，它提供用來建立封裝控制流程的設計介面，以及用來設定工作的自訂編輯器。 您也可以設計 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型的程式以程式設計方式建立封裝。  
  
## <a name="types-of-tasks"></a>工作的類型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括下列工作類型。  
  
 資料流程工作  
 執行資料流程以擷取資料、套用資料行層級轉換，以及載入資料的工作。  
  
 資料準備工作  
 這些工作會執行下列程序：複製檔案和目錄、下載檔案和資料、執行 Web 方法、將作業套用到 XML 文件，以及分析要清除的資料。  
  
 工作流程工作  
 與其他程序進行通訊以便執行封裝、執行程式或批次檔、在封裝之間傳送和接收訊息、傳送電子郵件、讀取 Windows Management Instrumentation (WMI) 資料，以及監看 WMI 事件的工作。  
  
 SQL Server 工作  
 存取、複製、插入、刪除以及修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件和資料的工作。  
  
 指令碼工作  
 使用指令碼擴充封裝功能的工作。  
  
 Analysis Services 工作  
 建立、修改、刪除以及處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的工作。  
  
 維護工作  
 執行管理功能如備份和壓縮 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫、重建和重新組織索引，以及執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 工作的工作。  
  
 自訂工作  
 此外，您可以使用支援 COM 的程式設計語言 (例如 Visual Basic) 或 .NET 程式設計語言 (例如 C#) 撰寫自訂工作。 如果您要在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中存取自訂工作，可為該工作建立及註冊使用者介面。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="configuration-of-tasks"></a>設定工作  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可包含單一工作，例如，在封裝執行時刪除資料庫資料表中各項記錄的執行 SQL 工作。 不過，封裝通常包含數項工作，且各項工作均設定為在封裝控制流程的內容中執行。 若事件處理常式為回應執行階段事件的工作流程，則亦可擁有工作。  
  
 如需使用 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 將工作加入封裝的詳細資訊，請參閱 [在控制流程中加入或刪除工作或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
 如需利用撰寫程式的方式將工作加入封裝的詳細資訊，請參閱 [以程式設計方式加入工作](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)。  
  
 每項工作均可使用 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 針對各項工作提供的自訂對話方塊，或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中包括的 [屬性] 視窗另行設定。 封裝可包括多項相同類型的工作，例如六項執行 SQL 工作，而每項工作皆可分別設定。 如需詳細資訊，請參閱 [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
## <a name="tasks-connections-and-groups"></a>工作連接和群組  
 如果工作包含超過一項工作，則會在控制流程中按照優先順序條件約束連接並排列順序。 如需詳細資訊，請參閱 [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md)。  
  
 您可將多項工作設為群組，並做為單一工作單位執行，或於迴圈中重複。 如需詳細資訊，請參閱 [Foreach 迴圈容器](../../integration-services/control-flow/foreach-loop-container.md)、 [For 迴圈容器](../../integration-services/control-flow/for-loop-container.md)和 [時序容器](../../integration-services/control-flow/sequence-container.md)。  
  
## <a name="related-tasks"></a>相關工作  
 [在控制流程中加入或刪除工作或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
  
