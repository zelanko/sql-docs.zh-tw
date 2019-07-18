---
title: 編輯 Oracle 資料庫屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraProp
ms.assetid: 58dc99f1-ee6b-4508-bb66-2bc589611ff7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e6ebbdd1f4df148d146393865039102af26b2984
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728896"
---
# <a name="edit-the-oracle-database-properties"></a>編輯 Oracle 資料庫屬性

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在屬性編輯器中使用 [Oracle] 索引標籤，以變更您在新增執行個體精靈中 [建立 CDC 資料庫] 頁面上提供的描述，以及變更 Oracle 記錄採礦資料庫連接資訊。  
  
 以下將描述 **[Oracle]** 索引標籤中的資訊。  
  
 **名稱**  
 您在新增執行個體精靈中 [建立 CDC 資料庫] 頁面上輸入的 CDC 執行個體名稱。 這個欄位是唯讀的，而且您無法編輯此資訊。  
  
 **說明**  
 您可以編輯新執行個體的描述，或者如果您在建立 CDC 執行個體時未加入描述，則可以加入描述。  
  
 **Oracle 連接字串**  
 電腦與您使用之 Oracle 資料庫之間的 Oracle 連接字串。 這個欄位是唯讀的，而且您無法編輯此資訊。 這是因為連接字串的某些變更可能會讓 Oracle CDC 執行個體完全指向另一個 Oracle 資料庫，因而損毀 **cdc.xdbcdc_config** 資料表中儲存的 CDC 執行個體狀態。 如果需要少量的變更，您可以直接在組態資料表中使用 SQL Server Management Studio 變更連接字串。  
  
 **Oracle 記錄採礦驗證**  
 若要針對包含記錄採礦者的 Oracle 資料庫輸入驗證認證，請在 [驗證]  底下選取下列其中一項：  
  
-   **Windows 驗證**：選取此選項可使用目前的 Windows 網域認證。 只有當設定 Oracle 資料庫使用 Windows 驗證時，才可使用這個選項。  
  
-   **Oracle 驗證**：如果您選取這個選項，您必須在您所連接的 Oracle 資料庫中鍵入使用者的 [使用者名稱]  和 [密碼]  。  
  
 您可以在檢視器中檢視 Oracle 資料庫屬性。 當使用檢視器時，此資訊是唯讀的。 檢視器也包括資料表中擷取的資料行清單。 如需有關如何存取此檢視器的詳細資訊，請參閱＜ [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [如何從 CDC 設計工具主控台管理 CDC 服務](../../integration-services/change-data-capture/how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [連接到 Oracle 來源資料庫](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md)   
 [連接到 Oracle](../../integration-services/change-data-capture/connect-to-oracle.md)  
  
  
