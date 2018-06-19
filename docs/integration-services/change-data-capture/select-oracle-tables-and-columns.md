---
title: 選取 Oracle 資料表和資料行 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 82bb01c13e4b011f74a0008e86dc1a05115d6abc
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402570"
---
# <a name="select-oracle-tables-and-columns"></a>選取 Oracle 資料表和資料行
  使用 [選取 Oracle 資料表和資料行] 頁面，從擷取變更的 Oracle 來源資料庫選取資料表。 此頁面具有以下元素：  
  
## <a name="options"></a>選項。  
 **資料表清單**  
 此資料表清單具有三個資料行：  
  
-   **Oracle 資料表名稱**：資料表的名稱，包括資料表結構描述。  
  
-   **擷取執行個體**：用來命名執行個體特有之異動資料擷取物件的擷取執行個體名稱。 擷取執行個體不得為 NULL。  
  
     如果沒有指定，就會採用 `<schema-name>_<table-name>`格式，從來源結構描述名稱加上來源資料表名稱衍生此名稱。 擷取執行個體名稱不得超過 100 個字元，而且在資料庫中必須是唯一的。  
  
     您可以在此資料行中按一下任何資料格，手動編輯 **capture_instance**。  
  
-   **安全性角色**：用來控制變更資料之存取權的資料庫控制角色名稱。  
  
     您可以在此資料行中按一下任何資料格，手動編輯 **security_role**。  
  
 **加入資料表**  
 按一下 [加入資料表] 開啟 [資料表選取範圍] 對話方塊，您可以在這裡[選取 Oracle 資料表來擷取變更](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)。  
  
 **編輯**  
 從清單中選取資料表，並選取 [編輯]，開啟該資料表的 [屬性] 對話方塊，您可以在這裡[變更為了擷取變更所選取的資料表](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)。  
  
 **移除**  
 從清單中選取資料表，並按一下 [移除]，從 CDC 執行個體中移除此資料表。  
  
 在您使用正確的對話方塊[選取 Oracle 資料表來擷取變更](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)及/或[變更為了擷取變更所選取的資料表](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)之後，請按一下 [下一步] [產生及執行補充記錄指令碼](../../integration-services/change-data-capture/generate-and-run-the-supplemental-logging-script.md)。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [編輯資料表](../../integration-services/change-data-capture/edit-tables.md)   
 [將資料表新增至 CDC 執行個體](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)   
 [編輯資料表屬性](../../integration-services/change-data-capture/edit-the-table-properties.md)  
  
  
