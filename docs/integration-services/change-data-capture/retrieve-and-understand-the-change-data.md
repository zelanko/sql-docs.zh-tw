---
title: 擷取與了解變更資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10b9057d6659ac37b0d841fa12549fdb8d3dc42f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="retrieve-and-understand-the-change-data"></a>擷取與了解變更資料
  在執行累加式變更資料載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中，第一個工作是執行可擷取變更資料的查詢。 您可以在「資料流程」工作的來源元件內部執行這個查詢。 然後，您可以使用下游轉換和目的地，將變更資料套用到您的目的地。  
  
> [!NOTE]  
>  建立包含資料表值函式的查詢是建立執行累加式變更資料載入之封裝程序的第三個步驟。 如需此查詢的詳細資訊，請參閱[建立函數以擷取變更資料](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)。 如需建立可執行累加式變更資料載入之封裝的完整程序描述，請參閱[異動資料擷取 &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)。  
  
## <a name="adding-the-data-flow-task"></a>加入資料流程工作  
 在封裝的資料流程中，您可以擷取異動資料、根據發生之變更的類型分隔資料列，然後將變更套用到目的地。  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>將資料流程工作加入至封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [控制流程] 索引標籤上，加入「資料流程」工作。  
  
2.  將準備查詢字串的先前工作連接到「資料流程」工作。  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>設定來源元件以查詢變更  
 來源元件會使用以變數準備並儲存的查詢字串，呼叫可擷取變更資料的資料表值函式。  
  
> [!NOTE]  
>  如需以變數準備並儲存之查詢字串的詳細資訊，請參閱 [準備查詢變更資料](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)。 如需擷取變更資料之資料表值函式的詳細資訊，請參閱 [建立函數以擷取變更資料](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)。  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>設定 OLE DB 來源以擷取變更資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [資料流程] 索引標籤上，加入 OLE DB 來源。  
  
2.  在 [OLE DB 來源編輯器] 的 [連線管理員] 頁面上，選取下列選項：  
  
    1.  將有效的連接設定到來源資料庫。  
  
    2.  針對 [資料存取模式]，選取 [來自變數的 SQL 命令]。  
  
    3.  針對 [變數名稱]，選取 [User::SqlDataQuery]。  
  
3.  在 [OLE DB 來源編輯器] 的 [資料行] 頁面上，確定您需要的所有資料行都對應到輸出資料行。  
  
## <a name="next-step"></a>下一個步驟  
 設定 OLE DB 來源以擷取變更資料後，下一個步驟是開始在封裝中設計資料流程。  
  
 **下一個主題** [處理插入、更新與刪除](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)  
  
  
