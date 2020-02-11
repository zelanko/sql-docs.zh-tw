---
title: 傳送 SQL Server 物件工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjectstask.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01b985a1bb818e7b3d3612596bb4e2b7fa6fd393
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62829468"
---
# <a name="transfer-sql-server-objects-task"></a>傳送 SQL Server 物件工作
  「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中的一個或多個類型物件。 例如，該工作可以複製資料表和預存程序。 因用作來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本不同，可複製不同類型的物件。 例如，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫包含結構描述和使用者定義彙總。  
  
## <a name="objects-to-transfer"></a>要傳送的物件  
 可以複製指定資料庫中的伺服器角色、角色和使用者，也可以複製所傳送物件的權限。 透過將相關聯的使用者、角色和權限與物件一起複製，可以讓所傳送物件立即可以在目的地伺服器上進行運作。  
  
 下表列出可複製的物件類型。  
  
|Object|  
|------------|  
|資料表|  
|檢視|  
|預存程序|  
|使用者定義的函式|  
|Defaults|  
|使用者自訂資料類型|  
|資料分割函數|  
|資料分割配置|  
|結構描述|  
|組件|  
|使用者定義彙總|  
|使用者定義類型|  
|XML 結構描述集合|  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之執行個體中建立的使用者定義類型 (UDT) 相依於 Common Language Runtime (CLR) 組件。 如果使用「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作傳送 UDT，您也必須設定該工作以傳送相依物件。 若要傳送相依物件，請將 `IncludeDependentObjects` 屬性設定為 `True`。  
  
### <a name="table-options"></a>資料表選項  
 複製資料表時，您可以指出要在複製處理中包含之資料表相關項目的類型。 您可以在複製相關資料表時一併複製下列類型的項目：  
  
-   索引  
  
-   觸發程序  
  
-   全文檢索索引  
  
-   主索引鍵  
  
-   外部索引鍵  
  
 您還可以指出工作所產生的指令碼是否為 Unicode 格式。  
  
## <a name="destination-options"></a>目的地選項  
 您可以設定「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作在傳送中包含結構描述名稱、資料、所傳送物件的擴充屬性和相依物件。 如果複製資料，則它可以取代或附加現有資料。  
  
 部分選項只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，僅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援結構描述。  
  
## <a name="security-options"></a>安全性選項  
 「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作可以包含來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫層級使用者和角色、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，以及所傳送物件的權限。 例如，傳送可以包含所傳送資料表的權限。  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>在 SQL Server 的執行個體之間傳送物件  
 「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作可支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的來源和目的地。  
  
## <a name="events"></a>事件  
 該工作會引發報告已傳送物件的資訊事件，並在覆寫物件時引發警告事件。 還會為動作 (例如，截斷資料庫資料表) 引發資訊事件。  
  
 「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作並不報告物件傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 `ExecutionValue` 屬性中儲存的執行值會傳回已傳送的物件數目。 透過將使用者自訂變數指派給「傳送 SQL Server 物件」工作的 `ExecValueVariable` 屬性，可將與物件傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送 SQL Server 物件」工作包含下列自訂記錄項目：  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects：此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects：此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外，`OnInformation` 事件的記錄項目會報告已為傳送選取之物件類型的物件數目、已傳送的物件數目，以及動作 (例如，隨資料表一同傳送資料時截斷資料表)。 為在目的地上覆寫的每個物件寫入 `OnWarning` 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 使用者必須具有在來源伺服器上瀏覽物件的權限，且必須具有在目的地伺服器上卸除和建立物件的權限，此外，使用者還必須能夠存取指定的資料庫和資料庫物件。  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>設定傳送 SQL Server 物件工作  
 可以設定「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作傳送所有物件、同一類型的所有物件，或只傳送同一類型的指定物件。 例如，您可以選擇只複製 AdventureWorks 資料庫中已選取的資料表。  
  
 如果「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作傳送資料表，則您可指定要隨該資料表一同複製之資料表相關物件的類型。 例如，您可以指定隨資料表一同複製的主索引鍵。  
  
 若要進一步加強所傳送物件的功能，您可以設定「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作在傳送中包含結構描述名稱、資料、所傳送物件的擴充屬性和相依物件。 複製資料時，您可以指定是取代還是附加現有資料。  
  
 在執行階段，「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作會使用兩個 SMO 連線管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作以外另行設定，然後在「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳輸 SQL Server 物件工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [傳送 SQL Server 物件工作編輯器 &#40;物件頁面&#41;](../transfer-sql-server-objects-task-editor-objects-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>以程式設計方式設定傳送 SQL Server 物件工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
