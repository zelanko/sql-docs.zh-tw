---
title: 專案導向的離線資料庫開發 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.general
- sql.data.tools.dbprojectwizard.summary
ms.assetid: e61e830d-9fcd-45e7-b7b4-93a42155dd56
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96effd7670d22461f6c347c9220f7a3c26b7f611
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624516"
---
# <a name="project-oriented-offline-database-development"></a>專案導向的離線資料庫開發
本節將說明 SQL Server Data Tools (SSDT) 所提供用於撰寫、建置、偵錯及發行資料庫專案的功能。  
  
使用 SSDT，您可以建立離線資料庫專案，而且不需連接到伺服器執行個體，即可透過在專案中加入、修改或刪除物件 (由指令碼代表) 的定義，來實作結構描述變更。 這些工作都可以透過使用資料表設計工具或 Transact\-SQL 編輯器來完成。 您還可以在相同專案中撰寫及偵錯 Transact\-SQL 和 CLR 物件。 您可以使用 [結構描述比較]，確保專案與生產資料庫保持同步，並在每個開發週期階段為專案建立快照集以利進行比較。 在以小組為主的環境下處理資料庫專案時，您可以利用所有檔案的版本控制。 在資料庫專案經過部署、測試及偵錯後，您可以將專案遞交給授權人員，以便發行至生產環境。  
  
> [!NOTE]  
> 本節的 HOW TO 主題包含一系列可依序完成的工作。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|---------|---------------|  
|[匯入資料庫專案中](../ssdt/import-into-a-database-project.md)|說明如何從即時資料庫、.dacpac 或指令碼匯入物件。|  
|[加入資料庫參考對話方塊](../ssdt/add-database-reference-dialog-box.md)|描述各種新增資料庫參考的方式。|  
|[檢查更新檔對話方塊](../ssdt/check-for-updates-dialog-box.md)|描述 SQL Server Data Tools 如何檢查產品更新。|  
|[資料庫專案設定](../ssdt/database-project-settings.md)|說明可控制資料庫與組建組態之各個部分的各種專案設定。|  
|[如何：瀏覽 SQL Server 資料庫專案中的物件](../ssdt/how-to-browse-objects-in-a-sql-server-database-project.md)|Visual Studio 的 SQL Server 物件總管現在包含專用的 [專案] 節點，在這個節點下方案的所有 SQL Server 資料庫專案都依 SQL Server Management Studio 類的階層分組。|  
|[資料工具作業視窗](../ssdt/data-tools-operations-window.md)|說明 [ **資料工具作業** ] 視窗，此視窗會顯示某些作業的進度，並在發生任何錯誤時通知您。|  
|[Transact-SQL 編輯器選項](../ssdt/transact-sql-editor-options.md)|描述 Transact\-SQL 選項。|  
|[如何：建立新的資料庫專案](../ssdt/how-to-create-a-new-database-project.md)|建立資料庫專案並匯入現有的資料庫結構描述。|  
|[如何：使用結構描述比較，比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)|比較資料庫與專案的結構描述並進行同步處理。|  
|[如何：建置及部署至本機資料庫](../ssdt/how-to-build-and-deploy-to-a-local-database.md)|使用本機指定的 SQL Server 執行個體，在偵測資料庫專案時會啟動這個執行個體。|  
|[如何：變更目標平台及發行資料庫專案](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)|將專案的目標 SQL Server 平台變更為任何支援的 SQL Server 執行個體，並驗證語法。|  
|[如何：建立專案的快照集](../ssdt/how-to-create-a-snapshot-of-a-project.md)|建立資料庫結構描述的唯讀 Proxy，並在不必要的變更套用到專案時還原來源專案。|  
|[如何：在專案中使用 Microsoft SQL Server 2012 物件](../ssdt/how-to-use-microsoft-sql-server-2012-objects-in-your-project.md)|將新的序列物件加入至專案。|  
|[如何：使用 CLR 資料庫物件](../ssdt/how-to-work-with-clr-database-objects.md)|在 SQL Server Data Tools 資料庫專案中建立及發行 CLR 物件。|  
|[如何：將 Visual Studio 2010 資料庫專案轉換成 SQL Server 資料庫專案並重定目標為不同平台](../ssdt/how-to-convert-visual-studio-2010-database-projects-to-ssql-server-projects.md)|將 Visual Studio 2010 中建立的現有 SQL Server 資料庫、CLR 物件和資料層應用程式專案轉換成 SQL Server Data Tools 資料庫專案。|  
|[如何：指定預先部署或部署後指令碼](../ssdt/how-to-specify-predeployment-or-postdeployment-scripts.md)|討論如何使用您想要在部署資料庫之前或之後執行的指令碼。|  
  
## <a name="related-sections"></a>相關章節  
[管理資料表、關聯性及修正錯誤](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
