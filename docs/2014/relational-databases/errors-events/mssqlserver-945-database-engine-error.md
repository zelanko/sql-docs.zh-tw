---
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 51284cdcf48f1bf713a853f9c87457cb5291cc4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053467"
---
# <a name="mssqlserver_945"></a>MSSQLSERVER_945
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|945|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DB_IS_SHUTDOWN|  
|訊息文字|檔案無法存取、記憶體或磁碟空間不足，因此無法開啟資料庫 '%.*ls'。  詳細資訊請參閱 SQL Server 錯誤記錄檔。|  
  
## <a name="explanation"></a>說明  
 資料庫無法存取，因為遺失檔案或其他資源。  
  
## <a name="user-action"></a>使用者動作  
 檢查錯誤記錄檔，以取得有關記憶體、磁碟空間或權限失敗的詳細資訊。 確認受影響資料庫的 .mdf 和 .ndf 檔案位置，並確認 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的帳戶有權限可以存取這些檔案。 更正問題之後，使用 ALTER DATABASE 將資料庫設定為 ONLINE，以重新啟動資料庫。  
  
  
