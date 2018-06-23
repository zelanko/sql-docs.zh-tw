---
title: 執行指令碼的 Oracle 認證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6d912497c755cafb9fd6a437e40944c0866b439b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147216"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  若要從 Oracle CDC 設計工具主控台執行 Oracle 補充記錄指令碼，此程式會提示您輸入執行此指令碼之 Oracle 使用者的認證。 若要執行此指令碼，Oracle 使用者必須擁有要擷取之所有資料表的 ALTER TABLE 權限以及 DBA_LOG_GROUPS 檢視表的 SELECT 權限。  
  
## <a name="task-list"></a>工作清單  
 請在此對話方塊中輸入以下資訊：  
  
 **驗證**  
  
 選取下列其中一項：  
  
-   **Windows 驗證**：選取此選項可使用目前的 Windows 網域認證。 只有當設定 Oracle 資料庫使用 Windows 驗證時，才可使用這個選項。  
  
-   **Oracle 驗證**：如果您選取這個選項，您必須在您所連接的來源 Oracle 資料庫中輸入使用者的 **[使用者名稱]** 和 **[密碼]** 。  
  
## <a name="see-also"></a>另請參閱  
 [如何管理 CDC 執行個體](manage-a-cdc-instance.md)   
 [檢閱及產生補充記錄指令碼](review-and-generate-supplemental-logging-scripts.md)  
  
  