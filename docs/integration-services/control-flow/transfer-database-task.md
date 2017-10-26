---
title: "傳送資料庫工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 29f66d1eeed7e2af0df962b62020169fb2095f6e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-database-task"></a>傳送資料庫工作
  「傳送資料庫」工作會在兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 與其他只能透過複製 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件來傳送它們的工作不同，「傳送資料庫」工作可以複製或移動資料庫。 這項工作也可用來在同一部伺服器內複製資料庫。  
  
## <a name="offline-and-online-modes"></a>離線和線上模式  
 資料庫可以使用線上或離線模式傳送。 當您使用線上模式時，資料庫會保持附加狀態，並使用 SQL Management Object (SMO) 複製資料庫物件來進行傳送。 當您使用離線模式時，會卸離資料庫，複製或移動資料庫檔案，並在傳送成功完成後將資料庫附加至目的地。 如果複製資料庫，則會在成功複製後將資料庫自動重新附加至來源。 在離線模式中，資料庫的複製速度會更快，但使用者在傳送期間無法使用資料庫。  
  
 離線模式需要您在包含資料庫檔案的來源和目的地伺服器上，指定網路檔案共用。 如果資料夾已共用，且可由使用者存取，則您可以使用語法 \\\computername\Program Files\myfolder\\參考網路共用。 否則，您必須使用語法 \\\computername\c$\Program Files\myfolder\\。 若要使用後面的語法，使用者必須具有來源和目的地網路共用的寫入權限。  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>在 SQL Server 的版本之間傳送資料庫  
 「傳送資料庫」工作可以在不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的執行個體之間，傳送資料庫。  
  
## <a name="events"></a>事件  
 「傳送資料庫」工作並不報告錯誤訊息傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 執行值 (在工作的 **ExecutionValue** 屬性中定義) 會傳回值 1，因為與其他傳送工作不同，「傳送資料庫」工作只能傳送一個資料庫。  
  
 透過將使用者定義變數指派給「傳送資料庫」工作的 **ExecValueVariable** 屬性，可將與錯誤訊息傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送資料庫」工作包含下列自訂記錄項目：  
  
-   SourceSQLServer    此記錄項目列出來源伺服器的名稱。  
  
-   DestSQLServer    此記錄項目列出目的地伺服器的名稱。  
  
-   SourceDB    此記錄項目列出傳送之資料庫的名稱。  
  
 另外，在覆寫目的地資料庫時，會寫入 **OnInformation** 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要使用離線模式傳送資料庫，執行封裝的使用者必須是 sysadmin 伺服器角色的成員。  
  
 若要使用線上模式傳送資料庫，執行封裝的使用者必須是 sysadmin 伺服器角色的成員，或是選取之資料庫的資料庫擁有者 (dbo)。  
  
## <a name="configuration-of-the-transfer-database-task"></a>傳送資料庫工作的組態  
 您可以指定如果資料庫傳送失敗，工作是否嘗試重新附加來源資料庫。  
  
 「傳送資料庫」工作還可設為允許覆寫具有相同名稱的目的地資料庫，以取代目的地資料庫。  
  
 來源資料庫還可以重新命名為傳送處理序的一部分。 如果您想要將資料庫傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目的地執行個體，而該執行個體已包含相同名稱的資料庫，則重新命名來源資料庫便可允許傳送資料庫。 不過，資料庫檔案名稱也必須不同，如果目的地上已存在具有相同名稱的資料庫檔案，則工作會失敗。  
  
 當您複製資料庫時，資料庫不能小於目的地伺服器上的 **model** 資料庫大小。 您可以增加要複製的資料庫大小，或減少 **model**的大小。  
  
 在執行階段，「傳送資料庫」工作會使用一或兩個 SMO 連接管理員，連接到來源和目的地伺服器。 當您在同一伺服器上建立資料庫的副本時，只需要一個 SMO 連接管理員。 SMO 連接管理員會在「傳送資料庫」工作以外另行設定，然後在「傳送資料庫」工作中參考。 當工作存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需相關資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>傳送資料庫工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>傳送資料庫工作編輯器 (一般頁面)
  使用 **[傳送資料庫工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名和描述傳送資料庫工作。 傳送資料庫工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的兩個執行個體間，複製或移動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 這項工作也可用來在同一部伺服器內複製資料庫。   
  
### <a name="options"></a>選項  
 **名稱**  
 為傳送資料庫工作輸入唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送資料庫工作的描述。  
  
## <a name="transfer-database-task-editor-databases-page"></a>傳送資料庫工作編輯器 (資料庫頁面)
  使用 [傳送資料庫工作編輯器] 對話方塊的 [資料庫] 頁面，即可指定傳送資料庫工作中所含之來源和目的地資料庫的屬性。 傳送資料庫工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的兩個執行個體間，複製或移動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 這項工作也可用來在同一部伺服器內複製資料庫。  
  
### <a name="options"></a>選項  
 **SourceConnection**  
 在清單中，選取一個 SMO 連接管理員，或按一下**\<新增連接 … >**來建立新的連接到來源伺服器。  
  
 **DestinationConnection**  
 在清單中，選取一個 SMO 連接管理員，或按一下**\<新增連接 … >**來建立新的連接到目的地伺服器。  
  
 **DestinationDatabaseName**  
 指定目的地伺服器上之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的名稱。  
  
 若要使用來源資料庫名稱來自動擴展此欄位，請先指定 **SourceConnection** 和 **SourceDatabaseName** 。  
  
 若要重新命名目的地伺服器上的資料庫，請在此欄位中輸入新名稱。  
  
 **DestinationDatabaseFiles**  
 指定目的地伺服器上之資料庫檔案的名稱和位置。  
  
 若要使用來源資料庫檔案的名稱和位置來自動擴展此欄位，請先指定 **SourceConnection**、 **SourceDatabaseName**和 **SourceDatabaseFiles** 。  
  
 若要重新命名資料庫檔案，或要指定目的地伺服器上的新位置，請使用來源資料庫的資訊來擴展此欄位，然後按一下瀏覽按鈕。 在 [目的地資料庫檔案] 對話方塊中，編輯 [目的地檔案]、[目的資料夾] 或 [網路檔案共用]。  
  
> [!NOTE]  
>  如果您是使用瀏覽按鈕找到資料庫檔案，就可以使用本機磁碟機代號來輸入檔案位置：例如 c:\\。 您必須以網路共用標記來取代此檔案位置，其中包含電腦名稱和共用名稱。 如果使用預設管理共用，您就必須使用 $ 標記，並具有管理權限存取該共用。  
  
 **DestinationOverwrite**  
 指定是否可以覆寫目的地伺服器上的資料庫。  
  
 此屬性具有下表所列的選項：  
  
|Value|說明|  
|-----------|-----------------|  
|**True**|覆寫目的地伺服器資料庫。|  
|**False**|請勿覆寫目的地伺服器資料庫。|  
  
> [!CAUTION]  
>  如果您為 **DestinationOverwrite** 指定了 **True**，此舉可能會造成資料遺失，且會覆寫目的地伺服器資料庫中的資料。 為了避免此情形發生，在執行傳送資料庫工作之前，請先將目的地伺服器資料庫備份至其他位置。  
  
 **動作**  
 指定工作會將資料庫 [複製] 或 [移動] 至目的地伺服器。  
  
 **方法**  
 指定當來源伺服器上的資料庫處於線上或離線模式時，是否會執行工作。  
  
 若要使用離線模式來傳送資料庫，執行封裝的使用者就必須是 **系統管理員** 固定伺服器角色的成員。  
  
 若要使用線上模式來傳送資料庫，執行封裝的使用者就必須是 **系統管理員** 固定伺服器角色的成員，或是選取之資料庫的資料庫擁有者 (**dbo**)。  
  
 **SourceDatabaseName**  
 選取要複製或移動之資料庫的名稱。  
  
 **SourceDatabaseFiles**  
 按一下瀏覽按鈕，即可選取資料庫檔案。  
  
 **ReattachSourceDatabase**  
 指定失敗發生時，工作是否會嘗試重新附加來源資料庫。  
  
 此屬性具有下表所列的選項：  
  
|Value|說明|  
|-----------|-----------------|  
|**True**|重新附加來源資料庫。|  
|**False**|請勿重新附加來源資料庫。|  

## <a name="source-database-files"></a>來源資料庫檔案
  使用 **[來源資料庫檔案]** 對話方塊，即可檢視來源伺服器上的資料庫檔案名稱和位置，或指定傳送資料庫工作的網路檔案共用位置。   
  
 若要以來源伺服器上的資料庫檔案名稱和位置來擴展此對話方塊，請在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，首先指定 **[SourceConnection]** 和 **[SourceDatabaseName]** 。  
  
### <a name="options"></a>選項。  
 **來源檔案**  
 在來源伺服器上，將會被傳送的資料庫檔案名稱。 **[來源檔案]** 是唯讀的。  
  
 **來源資料夾**  
 在來源伺服器上，要傳送之資料庫檔案所在的資料夾。 **[來源資料夾]** 是唯讀的。  
  
 **網路檔案共用**  
 在來源伺服器上，會從中傳送資料庫檔案的網路共用資料夾。 當您在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，將 **[方法]** 指定為 **[DatabaseOffline]** ，以離線模式傳送資料庫時，請使用 **[網路檔案共用]** 。  
  
 輸入網路檔案共用位置，或按一下 [瀏覽 (…)] 按鈕以尋找網路檔案共用位置。  
  
 在離線模式中傳送資料庫時，資料庫檔案會複製到來源伺服器上的 **[網路檔案共用]** 位置之後，才傳送到目的地伺服器。  

## <a name="destination-database-files"></a>目的地資料庫檔案
  使用 **[目的地資料庫檔案]** 對話方塊，即可檢視或變更目的地伺服器上的資料庫檔案名稱和位置，或是指定傳送資料庫工作的網路檔案位置。  
  
 若要使用來源伺服器上的資料庫檔案名稱和位置，來自動擴展此對話方塊，請先在 **[傳送資料庫工作編輯器]**對話方塊的 **[資料庫]**頁面中，指定 **[SourceConnection]** 、 **[SourceDatabaseName]** 和 **[SourceDatabaseFiles]** 。  
  
### <a name="options"></a>選項。  
 **目的地檔案**  
 目的地伺服器上已傳送資料庫檔案的名稱。  
  
 輸入檔案名稱，或是按一下檔案名稱來編輯它。  
  
 **目的資料夾**  
 目的地伺服器上的資料夾，用於存放將傳送的資料庫檔案。  
  
 輸入資料夾路徑，按一下該資料夾路徑來編輯它，或是按一下瀏覽來找出在目的地伺服器上的資料夾，以存放要傳送的資料庫檔案。  
  
 **網路檔案共用**  
 在目的地伺服器上的網路共用資料夾，其中存放要傳送的資料庫檔案。 當您在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，將 **[方法]** 指定為 **[DatabaseOffline]** ，以離線模式傳送資料庫時，請使用 **[網路檔案共用]** 。  
  
 輸入網路檔案共用位置，或是按一下瀏覽來找出網路檔案共用位置。  
  
 當您以離線模式傳送資料庫時，在將資料庫檔案傳送到 **[目的資料夾]** 位置之前，會將其複製到 **[網路檔案共用]** 位置。  

