---
title: 大量插入工作 | Microsoft Docs
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
- sql12.dts.designer.bulkinserttask.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 62
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4c21569df7269e7037befbe8fe190c9c84079e51
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209848"
---
# <a name="bulk-insert-task"></a>大量插入工作
  「大量插入」工作提供有效的方式，將大量資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檢視。 例如，假設您的公司將百萬個資料列的產品清單儲存在大型電腦系統上，但公司的電子商務系統是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴展網頁。 您必須在晚上以大型電腦的主產品清單更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品資料表。 若要更新資料表，請以 Tab 分隔的格式儲存產品清單，並使用「大量插入」工作將資料直接複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
  
 為了確保高速資料複製，從來源檔案將資料搬移到資料表或檢視時，無法執行資料的轉換。  
  
## <a name="usage-considerations"></a>使用狀況的考量  
 使用「大量插入」工作之前，請考慮下列事項：  
  
-   「大量插入」工作只能從文字檔將資料傳送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檢視。 若要使用「大量插入」工作傳輸來自其他資料庫管理系統 (DBMS) 的資料，您必須從來源將資料匯出到文字檔，然後從文字檔將資料匯入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檢視。  
  
-   目的地必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表或檢視。 若目的地資料表或檢視已經包含資料，則「大量插入」工作執行時，便會將新資料附加到現有資料中。 如果您要取代資料，請在執行「大量插入」工作之前，先執行會執行 DELETE 或 TRUNCATE 陳述式的執行 SQL 工作。 如需相關資訊，請參閱 [Execute SQL Task](execute-sql-task.md)。  
  
-   您可以在「大量插入」工作物件中使用格式檔案。 如果您已經有 **bcp** 公用程式所建立的格式檔，就可以在「大量插入」工作中指定它的路徑。 「大量插入」工作支援 XML 和非 XML 格式檔案。 如需格式檔案的詳細資訊，請參閱[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
-   只有系統管理員 (sysadmin) 固定伺服器角色的成員才能執行包含「大量插入」工作的封裝。  
  
## <a name="bulk-insert-task-with-transactions"></a>使用交易的大量插入工作  
 若未設定批次大小，則會將整個大量複製作業視為一項交易。 批次大小 **0** 表示會將資料插入一個批次中。 若有設定批次大小，則每一個批次即代表批次完成時的一筆認可交易。  
  
 「大量插入」工作的行為與交易相關，端視工作是否聯結封裝交易而定。 若「大量插入」工作並未聯結封裝交易，在嘗試下一個批次之前，會將每一個無錯誤的 (Error-free) 批次視為一個單位進行認可。 如果「大量插入」工作與封裝交易聯結，那麼工作結束時，無錯誤批次仍會保留在交易中。 這些批次是取決於封裝的認可或復原作業。  
  
 「大量插入」工作的錯誤不會自動復原已成功載入的批次；同樣地，如果工作成功，批次並不會自動認可。 認可和復原作業只會發生於回應封裝以及工作流程屬性設定的時候。  
  
## <a name="source-and-destination"></a>來源和目的地  
 當您指定文字來源檔的位置時，請考慮下列各項：  
  
-   伺服器必須有權限，才能同時存取檔案和目的地資料庫。  
  
-   伺服器會執行「大量插入」工作。 因此，該工作使用的任何格式檔案都必須位於伺服器上。  
  
-   「大量插入」工作載入的來源檔所在伺服器，可以和要插入資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫所在的伺服器相同，或位於遠端伺服器上。 如果檔案位於遠端伺服器上，則必須在路徑中指定使用「通用命名慣例」(UNC) 名稱的檔名。  
  
## <a name="performance-optimization"></a>效能最佳化  
 若要最佳化效能，請考慮下列各項：  
  
-   如果文字檔與要插入資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫位於同一台電腦上，則由於資料並非在網路上移動，因此複製作業進行的速度更快。  
  
-   「大量插入」工作不會記錄導致錯誤的資料列。 如果您必須擷取這項資訊，請使用資料流程元件的錯誤輸出擷取例外狀況檔案中造成錯誤的資料列。  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>大量插入工作上可用的自訂記錄項目  
 下表列出「大量插入」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`BulkInsertTaskBegin`|指出大量插入已經開始。|  
|`BulkInsertTaskEnd`|指出大量插入已經完成。|  
|`BulkInsertTaskInfos`|提供有關工作的描述性資訊。|  
  
## <a name="bulk-insert-task-configuration"></a>大量插入工作組態  
 您可以利用下列方式設定「大量插入」工作：  
  
-   指定讓 OLE DB 連接管理員連接到目的地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以及要插入資料的資料表或檢視。 「大量插入」工作只支援用於目的地資料庫的 OLE DB 連接。  
  
-   指定「檔案」或「一般檔案」連接管理員存取來源檔案。 「大量插入」工作僅針對來源檔案的位置，使用連接管理員。 此工作會忽略您在連接管理員編輯器中選取的其他選項。  
  
-   以格式檔案或定義來源資料之資料行和資料列的分隔符號，定義「大量插入」工作所使用的格式。 如果使用格式檔案，請指定讓「檔案」連接管理員存取該格式檔案。  
  
-   指定當工作插入資料時，要在目的地資料表或檢視上執行的動作。 這些選項包括是否檢查條件約束、啟用識別插入、保留 Null、引發觸發程序，或鎖定資料表。  
  
-   提供要插入的資料批次相關資訊，例如批次大小、要插入的檔案中的第一個和最後一個資料列、在工作停止插入資料列之前容許發生的插入錯誤數目，以及將進行排序的資料行名稱。  
  
 如果「大量插入」工作使用「一般檔案」連接管理員存取來源檔案，則該工作不會使用「一般檔案」連接管理員中指定的格式。 而「大量插入」工作會使用格式檔案中指定的格式，或工作之 RowDelimiter 和 ColumnDelimiter 屬性的值。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [大量插入工作編輯器&#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [大量插入工作編輯器&#40;連接頁面&#41;](../bulk-insert-task-editor-connection-page.md)  
  
-   [大量插入工作編輯器&#40;選項頁面&#41;](../bulk-insert-task-editor-options-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>大量插入工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>相關工作  
 [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>相關內容  
  
-   support.microsoft.com 上的技術文件： [您可能會在啟用 UAC 的系統上收到「無法準備 SSIS 大量插入來進行資料插入」錯誤](http://go.microsoft.com/fwlink/?LinkId=233693)。  
  
-   msdn.microsoft.com 上的技術文章： [資料載入效能指南](http://go.microsoft.com/fwlink/?LinkId=233700)。  
  
-   simple-talk.com 上的技術文件： [Using SQL Server Integration Services to Bulk Load Data](http://go.microsoft.com/fwlink/?LinkId=233701)(使用 SQL Server Integration Services 大量載入資料)。  
  
  
