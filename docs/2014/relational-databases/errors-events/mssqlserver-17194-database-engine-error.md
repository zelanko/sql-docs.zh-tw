---
title: MSSQLSERVER_17194 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d5425431d465c9bddba23c959aab41cefbfcdd89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915327"
---
# <a name="mssqlserver17194"></a>MSSQLSERVER_17194
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17194|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|伺服器無法載入登入所需的 SSL 提供者程式庫，此連接已經關閉。 SSL 可用來加密登入順序或所有通訊，視管理員對伺服器所做的設定而定。 如需有關此錯誤訊息資訊，請參閱線上叢書 》:0xXXXX. [用戶端：11.11.11.11]|  
  
## <a name="explanation"></a>說明  
 這個錯誤表示用戶端已經關閉連接。 發生這個錯誤是因為連接逾時期限已到。 錯誤訊息中顯示的值來自作業系統，提供基礎問題的說明。  
  
## <a name="user-action"></a>使用者動作  
 如果訊息中的錯誤碼是 0x2746 (十進位值 10054)，即表示用戶端已經重設連接，通常是因為逾時之故。若要解決錯誤，請增加用戶端或呼叫端程式的連接逾時值。  
  
 如需得知其他錯誤訊息值可行的解決方案，請使用作業系統命令 **net helpmsg** 並指定錯誤碼的十進位值。  
  
 如需如何連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的詳細資訊，請參閱[伺服器網路組態](../../database-engine/configure-windows/server-network-configuration.md)和[用戶端網路組態](../../database-engine/configure-windows/client-network-configuration.md)。  
  
## <a name="internal-only"></a>僅供內部使用  
  
