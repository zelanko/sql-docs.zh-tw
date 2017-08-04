---
title: "SQL Server 目的地 |Microsoft 文件"
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
- sql13.dts.designer.sqlserverdest.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
caps.latest.revision: 65
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f1224814d165d5763d832b18f6523c6c47f6f59c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="sql-server-destination"></a>SQL Server 目的地
  SQL Server 目的地會連接到本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，並大量載入資料到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表和檢視中。 如果封裝會存取遠端伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，您就無法在這種封裝中使用 SQL Server 目的地。 反之，這種封裝應該使用 OLE DB 目的地。 如需詳細資訊，請參閱 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)。  
  
## <a name="permissions"></a>Permissions  
 使用者必須擁有「建立全域物件」權限，才能執行包含 SQL Server 目的地的封裝。 您可以使用「本機安全性原則」工具 (從 [系統管理工具] 功能表中開啟) 將此權限授與使用者。 如果您在執行使用 SQL Server 目的地的封裝時收到錯誤訊息，請確定執行該封裝的帳戶是否擁有「建立全域物件」權限。  
  
## <a name="bulk-inserts"></a>大量插入  
 如果您嘗試使用 SQL Server 目的地將資料大量載入遠端 SQL Server 資料庫，可能會看到類似下面這樣的錯誤訊息：「有 OLE DB 記錄可用」。 來源："Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 描述: 「無法大量載入，因為無法開啟 SSIS 檔案對應物件 'Global\DTSQLIMPORT」。 作業系統錯誤碼 2 (系統找不到指定的檔案)。 請確定是透過 Windows 安全性存取本機伺服器」。  
  
 與「大量插入」工作一樣，SQL Server 目的地也可以對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進行相同的高速資料插入；不過，透過使用 SQL Server 目的地，在資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，封裝可以將轉換套用到資料行資料。  
  
 若要將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您應該考慮使用 SQL Server 目的地，而不是 OLE DB 目的地。  
  
### <a name="bulk-insert-options"></a>大量插入選項  
 如果 SQL Server 目的地使用快速載入資料存取模式，則您可以指定下列快速載入選項：  
  
-   保留匯入資料檔中的識別值或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指派的唯一值。  
  
-   大量載入作業期間保留 Null 值。  
  
-   大量匯入作業期間驗證目標資料表或檢視的條件約束。  
  
-   大量載入作業期間需要資料表層級鎖定。  
  
-   大量載入作業期間執行目的地資料表上定義的插入觸發器。  
  
-   在大量插入作業期間，指定輸入中要載入的第一個資料列編號。  
  
-   大量插入作業期間指定要載入之輸入的最後一個資料列編號。  
  
-   指定在取消大量載入作業之前，允許發生錯誤的最多數目。 每個無法匯入的資料列都將算為一個錯誤。  
  
-   指定輸入中包含已排序資料的資料行。  
  
 如需大量載入選項的詳細資訊，請參閱 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
#### <a name="performance-improvements"></a>效能改進  
 若要提升大量插入以及大量插入作業期間存取資料表資料的效能，您應該變更預設選項，如下：  
  
-   大量匯入作業期間不驗證目標資料表或檢視的條件約束。  
  
-   大量載入作業期間不執行目的地資料表上定義的插入觸發器。  
  
-   不要將鎖定套用到資料表。 這樣，在大量插入作業期間，其他使用者和應用程式依然可以使用該資料表。  
  
## <a name="configuration-of-the-sql-server-destination"></a>SQL Server 目的地的組態  
 您可以利用下列方式設定 SQL Server 目的地：  
  
-   指定要大量載入資料的資料表或檢視。  
  
-   透過指定一些選項 (例如是否要檢查條件約束的選項) 來自訂大量載入作業。  
  
-   指定所有資料列是以一個批次認可，或設定每個批次所認可的最大資料列數。  
  
-   指定大量載入作業的逾時。  
  
 此目的地使用 OLE DB 連接管理員連接到資料來源，且連接管理員會指定要使用的 OLE DB 提供者。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案還會提供資料來源物件，您可以從中建立 OLE DB 連接管理員。 這樣就可以向 SQL Server 目的地提供資料來源和資料來源檢視。  
  
 SQL Server 目的地有一個輸入。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可以在 [SQL Server 目的地編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [SQL 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sql-destination-editor-connection-manager-page.md)  
  
-   [SQL 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)  
  
-   [SQL 目的地編輯器 &#40;進階頁面&#41;](../../integration-services/data-flow/sql-destination-editor-advanced-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [SQL Server 目的地自訂屬性](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用 SQL Server 目的地來大量載入資料](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 SQL Server 目的地來大量載入資料](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
  
-   support.microsoft.com 上的技術文件： [You may get "Unable to prepare the SSIS bulk insert for data insertion" error on UAC enabled systems](http://go.microsoft.com/fwlink/?LinkId=199482)(您可能會在啟用 UAC 的系統上收到「無法準備 SSIS 大量插入來進行資料插入」錯誤)。  
  
-   msdn.microsoft.com 上的技術文章： [資料載入效能指南](http://go.microsoft.com/fwlink/?LinkId=233700)。  
  
-   simple-talk.com 上的技術文件： [Using SQL Server Integration Services to Bulk Load Data](http://go.microsoft.com/fwlink/?LinkId=233701)。  
  
## <a name="see-also"></a>請參閱＜  
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
