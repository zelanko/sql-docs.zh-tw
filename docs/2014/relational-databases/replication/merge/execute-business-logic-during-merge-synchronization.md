---
title: 在合併同步處理期間執行商務邏輯 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom error resolution [SQL Server replication]
- custom change handling [SQL Server replication]
- errors [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
ms.assetid: 9d4da2ef-c17f-4a31-a1f6-5c3b7ca85f71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 440419f1fb4670ff5bdfc2e49cd9cfe6fa5df65e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62999569"
---
# <a name="execute-business-logic-during-merge-synchronization"></a>在合併同步處理期間執行商務邏輯
  商務邏輯處理常式架構允許您撰寫在合併同步處理過程中呼叫的 Managed 程式碼組件。 組件包括可對應至幾種同步處理條件的商務邏輯：資料變更、衝突和錯誤。 商務邏輯處理常式架構提供了簡單的程式設計模型，且合併處理為您組件提供的資料是 ADO.NET 資料集的形式，因此您可以利用 ADO.NET 知識而無需了解專屬介面。 如需程式設計商務邏輯處理常式的詳細資訊，請參閱：  
  
-   應用程式開發介面 (API) 參考： <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>  
  
-   如何實作商務邏輯處理常式的指示：[為合併發行項實作商務邏輯處理常式](../implement-a-business-logic-handler-for-a-merge-article.md)  
  
## <a name="uses-for-business-logic-handlers"></a>商務邏輯處理常式的使用  
 合併同步處理可以叫用商務邏輯處理常式以執行下列作業：  
  
-   自訂變更處理  
  
-   自訂衝突解決方案  
  
-   自訂錯誤解決方案  
  
> [!NOTE]  
>  指定的商務邏輯處理常式會針對要同步處理的每一個資料列執行。 對其他應用程式或網路服務的複雜邏輯與呼叫可能會影響效能。  
  
### <a name="custom-change-handling"></a>自訂變更處理  
 商務邏輯處理常式可以在處理相互不衝突的資料變更期間叫用，並可執行下列三個動作之一：  
  
-   拒絕資料  
  
     這對不想與給定「訂閱者」進行變更傳播的應用程式非常有用。 例如，管理員可以篩選出不屬於「訂閱者」資料分割的插入，或拒絕在「訂閱者」端執行的刪除。 另一個範例是，當庫存無法再使用時，應用程式可以拒絕在「訂閱者」端輸入的訂單。  
  
-   接受資料  
  
     這對於在允許對「發行者」或「訂閱者」端所作的資料變更進行傳播之前，必須檢閱這些變更的應用程式非常有用。 例如，中層應用程式可以檢查來自現場的新訂單，並與中層採購工作流程處理整合在一起。  
  
-   套用自訂資料  
  
     這對於需要覆寫特定資料值或作業的應用程式非常有用。 例如，應用程式可以將資料列刪除轉換至資料列之 **status** 資料行設定為「已刪除」值的特殊更新，然後追蹤執行刪除的用戶端識別。 可用於稽核或工作流程。  
  
### <a name="custom-conflict-resolution"></a>自訂衝突解決方案  
 合併式複寫提供了衝突偵測和解決，可讓您接受預設解決策略或選取自訂的衝突解決方案。 如需詳細資訊，請參閱[Advanced Merge Replication 衝突偵測和解決](advanced-merge-replication-conflict-detection-and-resolution.md)方式。 商務邏輯處理常式可以在處理衝突的資料變更期間叫用，並可執行下列兩個動作之一：  
  
-   接受預設解決方案  
  
     這對於可能需要檢閱衝突、執行其他動作以及記錄自訂衝突記錄檔訊息的應用程式非常有用。  
  
-   執行自訂解決方案  
  
     這適用於可能需要針對商務邏輯選取特定資料值，而且會在自訂資料集內提供同步處理流程的應用程式。 例如，應用程式可以透過將「發行者」和「訂閱者」資料集的值進行組合，提供新版的優先資料列。  
  
### <a name="custom-error-resolution"></a>自訂錯誤解決方案  
 在傳播產生錯誤的變更時可以叫用自訂邏輯。 此邏輯可以執行下列兩個動作之一：  
  
-   接受預設錯誤解決方案  
  
     這對於可能需要檢閱錯誤、執行其他動作以及記錄自訂錯誤記錄檔訊息的應用程式非常有用。  
  
-   接受自訂錯誤解決方案  
  
     這適用於可能需要針對商務邏輯選取特定資料值，而且會在自訂資料集內提供同步處理流程的應用程式。 例如，當複寫處理遇到重複索引鍵違規時，商務邏輯處理常式可以提供新版的資料變更，其中的索引鍵將不再發生衝突。 隨後在「發行者」與「訂閱者」端所作的變更仍將保存在資料庫中，且複寫處理不必以刪除來補償失敗的插入。  
  
## <a name="deployment-scenarios-for-business-logic-handlers"></a>商務邏輯處理常式的部署案例  
 商務邏輯處理常式可以部署在：  
  
-   散發者。 使用發送訂閱，以便在「散發者」端執行商務邏輯。  
  
-   「訂閱者」端。 使用提取訂閱，以便在「訂閱者」端執行商務邏輯。  
  
-   Internet Information Services (IIS) 伺服器，如果使用 Web 同步處理。 使用與 Web 同步處理同步的提取訂閱，且商務邏輯處理常式將在 IIS Server 端執行。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫](merge-replication.md)   
 [訂閱發行集](../subscribe-to-publications.md)   
 [同步處理資料](../synchronize-data.md)   
 [合併式複寫的 Web 同步處理](../web-synchronization-for-merge-replication.md)  
  
  
