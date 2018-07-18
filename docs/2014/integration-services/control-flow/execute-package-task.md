---
title: 執行套件工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.f1
helpviewer_keywords:
- Execution Package task [Integration Services]
- child packages
- parent packages [Integration Services]
ms.assetid: 042d4ec0-0668-401c-bb3a-a25fe2602eac
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 256a7cbabc6c07bb0e1f42aeb6a3a3d77a5d93a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171139"
---
# <a name="execute-package-task"></a>執行封裝工作
  「執行封裝」工作可讓封裝將其他封裝當做工作流程的一部分執行，以延伸 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的企業功能。  
  
 您可將「執行封裝」工作用於下列用途：  
  
-   細分複雜的封裝工作流程。 此工作可讓您將工作流程分解成多個封裝，以方便讀取、測試和維護。 例如，您若是將資料載入星狀結構描述，就可以建立另一個封裝以擴展每一個維度與事實資料表。  
  
-   重複使用部分封裝。 其他封裝可以重複使用封裝工作流程的各部分。 例如，您可以建置可從不同封裝呼叫的資料擷取模組。 呼叫擷取模組的每個封裝可以執行不同的資料刪除、篩選或彙總作業。  
  
-   群組工作單位。 工作的單位可以封裝到個別的封裝，並以交易式元件聯結至父封裝的工作流程。 例如，父封裝執行附帶封裝，並根據附帶封裝的成功或失敗認可或回復交易。  
  
-   控制封裝安全性。 封裝作者只需要多封裝方案的一部分存取權。 您可藉由將封裝分成多個封裝，提供更高的安全性等級，這是因為您可以只將相關封裝的存取權授與給作者。  
  
 執行其他封裝的封裝一般稱為父封裝，而父工作流程執行的封裝則稱為子封裝。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含執行工作流程作業的工作，例如執行可執行檔和批次檔。 如需詳細資訊，請參閱＜ [Execute Process Task](execute-process-task.md)＞。  
  
## <a name="running-packages"></a>執行封裝  
 「執行封裝」工作可以執行包含父封裝之相同專案中所含的子封裝。 您可以透過將 **[ReferenceType]** 屬性設定為 **[專案參考]**，然後設定 **[PackageNameFromProjectReference]** 屬性，以便從專案中選取子封裝。  
  
> [!NOTE]  
>  [ReferenceType] 選項是唯讀的，如果尚未將包含封裝的專案轉換為專案部署模型，則該選項設為 [外部參考]。 如需轉換的詳細資訊，請參閱 [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md) (將專案部署至 Integration Services 伺服器)。  
  
 「執行封裝」工作也可執行儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 資料庫中的封裝，以及儲存在檔案系統中的封裝。 此工作使用 OLE DB 連接管理員連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，或使用檔案連接管理員存取檔案系統。 如需詳細資訊，請參閱＜ [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) ＞和＜ [Flat File Connection Manager](../connection-manager/flat-file-connection-manager.md)＞。  
  
 「執行封裝」工作也可執行資料庫維護計畫，讓您管理相同 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 方案中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝和資料庫維護計畫。 資料庫維護計畫與 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝類似，不過計畫只能包含資料庫維護工作，而且一律儲存在 msdb 資料庫中。  
  
 如果您選擇儲存在檔案系統中的封裝，就必須提供封裝的名稱與位置。 封裝可存在於檔案系統中的任何位置，不必與父封裝位在相同資料夾中。  
  
 子封裝可在父封裝的處理序中執行，也可在其自己的處理序中執行。 在其自己的處理序中執行子封裝需要更多記憶體，但是提供更大彈性。 例如，如果子處理序失敗，父處理序可繼續執行。  
  
 或者，有時您可能希望父封裝和子封裝當作一個單位一起失敗，或是不要產生其他處理序的額外負擔。 例如，如果子處理序失敗，而父封裝處理序中的後續處理取決於子處理序的成功，則子封裝應該在父封裝的處理序中執行。  
  
 根據預設，「 執行封裝 」 工作的 ExecuteOutOfProcess 屬性設為`False`，並執行相同的處理序與父封裝中的子封裝。 如果您將此屬性設定為 `True`，子封裝就會在不同的處理序中執行。 這可能會降低子封裝的啟動速度。 此外，如果您將屬性設定為`True`，您無法偵錯僅限工具安裝中的封裝。 您必須安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 如需詳細資訊，請參閱 [安裝 Integration Services](../install-windows/install-integration-services.md)。  
  
## <a name="extending-transactions"></a>延伸交易  
 父封裝使用的交易可延伸至子封裝；因此，這兩種封裝執行的工作都能認可或回復。 例如，根據子封裝執行的資料庫插入，可以認可或回復父封裝所執行的資料庫插入，反之亦然。 如需詳細資訊，請參閱＜ [Inherited Transactions](../inherited-transactions.md)＞。  
  
## <a name="propagating-logging-details"></a>傳播記錄詳細資料  
 「執行封裝」工作執行的子封裝不一定會設定為使用記錄，但是子封裝永遠會將記錄的詳細資料轉送給父封裝。 如果「執行封裝」工作設定為使用記錄，則此工作會記錄來自子封裝的記錄詳細資料。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)。  
  
## <a name="passing-values-to-child-packages"></a>將值傳遞給子封裝  
 子封裝通常使用由另一個呼叫它的封裝傳遞給它的值，該封裝一般是其父封裝。 使用來自父封裝的值在下列類似狀況中很有用：  
  
-   將較大工作流程的各個部分指派給不同的封裝。 例如，一個封裝每晚下載資料、摘要資料、指派摘要資料值給變數，然後將值傳遞給另一個封裝進行資料的額外處理。  
  
-   父封裝會動態協調子封裝中的工作。 例如，父封裝決定本月的天數，並將該數字指派給變數，然後由子封裝執行該次數的工作。  
  
-   子封裝需要存取由父封裝動態衍生的資料。 例如，父封裝會從資料表擷取資料並將資料列集載入變數，子封裝則會對該資料執行其他作業。  
  
 您可以使用下列方法，將值傳遞至子封裝：  
  
-   **封裝組態**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供「父封裝變數」組態的組態類型，可將值從父封裝傳遞至子封裝。 組態建立在子封裝上，並使用父封裝中的變數。 然後，組態會對應至子封裝中的變數，或是子封裝中的物件屬性。 變數也可用在指令碼工作或指令碼元件所用的指令碼中。  
  
-   **參數**  
  
     您可以設定「執行封裝」工作將父封裝變數或參數 (或專案參數) 對應到子封裝參數。 專案必須使用專案部署模型，而且子封裝必須包含在包含父封裝的相同專案中。 如需詳細資訊，請參閱＜ [Execute Package Task Editor](../execute-package-task-editor.md)＞。  
  
    > [!NOTE]  
    >  如果子封裝參數不區分大小寫，但對應到區分大小寫的父參數，則子封裝將無法執行。  
    >   
    >  支援下列對應條件：  
    >   
    >  -   區分大小寫，子封裝參數對應到區分大小寫的父參數  
    > -   區分大小寫，子封裝參數對應到不區分大小寫的父參數  
    > -   不區分大小寫，子封裝參數對應到不區分大小寫的父參數  
  
 父封裝變數可在「執行封裝」工作的範圍內定義，或是在諸如封裝的父容器中定義。 如果有多個名稱相同的變數可用，則會使用在「執行封裝」工作範圍內所定義的變數，或是最接近工作範圍的變數。  
  
 如需詳細資訊，請參閱 [Use the Values of Variables and Parameters in a Child Package](../use-the-values-of-variables-and-parameters-in-a-child-package.md)(在子封裝中使用變數和參數的值)。  
  
### <a name="accessing-parent-package-variables"></a>存取父封裝變數  
 子封裝可藉由使用指令碼工作存取父封裝變數。 當你在 **[指令碼工作編輯器]** 的 **[指令碼]** 頁面上輸入父封裝變數的名稱時，變數名稱中請勿加上 **User:** 。 否則，在您執行父封裝時子封裝會找不到該變數。 如需使用指令碼工作存取父封裝變數的詳細資訊，請參閱此部落格文章[SSIS： 存取父封裝中的變數](http://go.microsoft.com/fwlink/?LinkId=257729)，consultingblogs.emc.com 上。  
  
## <a name="configuring-the-execute-package-task"></a>設定執行封裝工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [執行套件工作編輯器](../execute-package-task-editor.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>相關工作  
  
## <a name="related-content"></a>相關內容  
  
-   部落格文章[SSIS： 應執行同處理序或跨處理序的子封裝？](http://go.microsoft.com/fwlink/?LinkId=220819)，consultingblogs.emc.com 上。  
  
-   部落格文章[SSIS： 存取父封裝中的變數](http://go.microsoft.com/fwlink/?LinkId=257729)，consultingblogs.emc.com 上。  
  
  
