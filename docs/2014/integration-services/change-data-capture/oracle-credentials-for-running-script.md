---
title: 執行指令碼的 Oracle 認證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12de97bf147ccb61cde5f82e2fa31782404071e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771109"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  若要從 Oracle CDC 設計工具主控台執行 Oracle 補充記錄指令碼，此程式會提示您輸入執行此指令碼之 Oracle 使用者的認證。 若要執行此指令碼，Oracle 使用者必須擁有要擷取之所有資料表的 ALTER TABLE 權限以及 DBA_LOG_GROUPS 檢視表的 SELECT 權限。  
  
## <a name="task-list"></a>工作清單  
 請在此對話方塊中輸入以下資訊：  
  
 **驗證**  
  
 選取下列其中一個：  
  
-   **Windows 驗證**：選取此選項可使用目前的 Windows 網域認證。 只有當設定 Oracle 資料庫使用 Windows 驗證時，才可使用這個選項。  
  
-   **Oracle 驗證**：如果您選取這個選項，您必須在您所連接的來源 Oracle 資料庫中輸入使用者的 **[使用者名稱]** 和 **[密碼]** 。  
  
## <a name="see-also"></a>另請參閱  
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [檢閱及產生補充記錄指令碼](review-and-generate-supplemental-logging-scripts.md)  
  
  
