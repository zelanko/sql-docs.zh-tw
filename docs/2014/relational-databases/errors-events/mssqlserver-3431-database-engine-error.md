---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 02724ea8bf358294af5e5dcd6c8f549d80010391
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426457"
---
# <a name="mssqlserver3431"></a>MSSQLSERVER_3431
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|3431|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|UNRESOLVED_XACT|  
|訊息文字|無法復原資料庫 '%.*ls' (資料庫識別碼 %d)，因為有尚未解決的交易結果。 Microsoft 分散式交易協調器 (MS DTC) 的交易已備妥，但 MS DTC 無法決定解決方式。 若要解決，必須修正 MS DTC、從完整備份還原，或者修復資料庫。|  
  
## <a name="explanation"></a>說明  
 資料庫關閉時，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 的一個或多個分散式交易未完成。 由於無法從 MS DTC 取得更多資訊，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法完成交易或回復交易，因此，此資料庫的復原失敗。  
  
## <a name="user-action"></a>使用者動作  
 若要復原此資料庫，您必須先解決 MS DTC 的問題。 若要調查 MS DTC 的問題，請檢查 Windows 事件記錄檔。 如果無法解決 MS DTC 問題並復原資料庫，請還原資料庫備份。  
  
  
