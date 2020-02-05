---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 921dde33b466cf9f72a8254f304d2a0abd739f7e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132394"
---
# <a name="mssqlserver_3431"></a>MSSQLSERVER_3431
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3431|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|UNRESOLVED_XACT|  
|訊息文字|無法復原資料庫 '%.*ls' (資料庫識別碼 %d)，因為有尚未解決的交易結果。 Microsoft 分散式交易協調器 (MS DTC) 的交易已備妥，但 MS DTC 無法決定解決方式。 若要解決，必須修正 MS DTC、從完整備份還原，或者修復資料庫。|  
  
## <a name="explanation"></a>說明  
資料庫關閉時，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 的一個或多個分散式交易未完成。 由於無法從 MS DTC 取得更多資訊，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法完成交易或回復交易，因此，此資料庫的復原失敗。  
  
## <a name="user-action"></a>使用者動作  
若要復原此資料庫，您必須先解決 MS DTC 的問題。 若要調查 MS DTC 的問題，請檢查 Windows 事件記錄檔。 如果無法解決 MS DTC 問題並復原資料庫，請還原資料庫備份。  
  
