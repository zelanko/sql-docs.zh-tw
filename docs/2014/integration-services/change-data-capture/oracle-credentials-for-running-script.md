---
title: 執行指令碼的 Oracle 認證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca3f76c49b950f6830c4d60f011bbdb158055179
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796090"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  若要從 Oracle CDC 設計工具主控台執行 Oracle 補充記錄指令碼，此程式會提示您輸入執行此指令碼之 Oracle 使用者的認證。 若要執行此指令碼，Oracle 使用者必須擁有要擷取之所有資料表的 ALTER TABLE 權限以及 DBA_LOG_GROUPS 檢視表的 SELECT 權限。  
  
## <a name="task-list"></a>工作清單  
 請在此對話方塊中輸入以下資訊：  
  
 **驗證**  
  
 選取下列其中一項：  
  
-   **Windows 驗證**:選取此選項可使用目前的 Windows 網域認證。 只有當設定 Oracle 資料庫使用 Windows 驗證時，才可使用這個選項。  
  
-   **Oracle 驗證**:如果您選取此選項時，您必須輸入**使用者名**並**密碼**如您所連接的來源 Oracle 資料庫中的使用者。  
  
## <a name="see-also"></a>另請參閱  
 [如何管理 CDC 執行個體](manage-a-cdc-instance.md)   
 [檢閱及產生補充記錄指令碼](review-and-generate-supplemental-logging-scripts.md)  
  
  
