---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 763ab2f136f76a1fa4a6e490f109c1ac47c87ff0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031883"
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1401|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_MASTERSTARTUP|  
|訊息文字|資料庫鏡像主執行緒常式啟動失敗，原因如下: %ls。 請更正錯誤的原因，然後重新啟動 SQL Server 服務。|  
  
## <a name="explanation"></a>說明  
 鏡像控制執行緒啟動失敗。  
  
## <a name="user-action"></a>使用者動作  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄中，尋找在此訊息之前發生的相關錯誤。 請更正錯誤的原因，然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務 (MSSQLSERVER)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  