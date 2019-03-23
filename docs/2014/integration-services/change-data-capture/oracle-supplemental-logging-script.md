---
title: Oracle 補充記錄指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5e6ee618-b89b-46c7-92ad-4fc5ef7b777a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c8f876852ff78e254bdff7ed687d2196d01d9c1d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379169"
---
# <a name="oracle-supplemental-logging-script"></a>Oracle 補充記錄指令碼
  此對話方塊會顯示 Oracle 補充記錄指令碼。  
  
 當您準備要使用的 CDC 執行個體時，CDC 設計工具會建立 Oracle SQL 指令碼，該指令碼會針對要擷取的資料表設定補充記錄。 補充記錄指令碼會告知 Oracle 何時更新特定資料表，而且它寫入交易記錄中的變更記錄應該包含所有相關之資料行的資料，而不只是變更的資料行。  
  
 根據組織內的 Oracle DBA 政策而定，執行補充記錄指令碼可能需要 Oracle DBA 審查及核准。  
  
## <a name="options"></a>選項。  
 以下是如何執行指令碼的可用選項。  
  
 **執行指令碼**  
 在針對 CDC 執行個體定義的資料表上執行補充記錄指令碼。 若要執行此指令碼，Oracle 使用者必須擁有要擷取之所有資料表的 ALTER TABLE 權限以及 DBA_LOG_GROUPS 檢視表的 SELECT 權限。 此外，Oracle 使用者必須擁有使用 Oracle 資料庫之必要權限的認證。 您可以讓程式提示您輸入 Oracle 認證，然後讓它執行指令碼。  
  
 **另存新檔**  
 將指令碼儲存至文字檔。 如果 Oracle 資料庫管理員 (DBA) 需要檢查及執行補充記錄指令碼，就會使用這個方式。此程式可讓您將指令碼儲存成文字檔，之後可以將此文字檔透過電子郵件或其他方式傳送給 Oracle DBA 以供日後執行 (使用 SQL*Plus Oracle 公用程式或其他工具，在 Oracle 資料庫上執行指令碼)。  
  
 **[複製]**  
 將指令碼複製到剪貼簿。 備妥之後，您可以將指令碼貼到所需的任何位置，萬一 Oracle 資料庫管理員 (DBA) 需要檢查及執行補充記錄指令碼時，就可以派上用場。  
  
## <a name="see-also"></a>另請參閱  
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [管理 CDC 執行個體](manage-a-cdc-instance.md)  
  
  
