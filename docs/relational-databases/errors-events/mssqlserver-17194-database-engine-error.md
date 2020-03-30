---
title: MSSQLSERVER_17194 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 47678d81d2868af5a921d26f3e121837a1ddc938
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68131734"
---
# <a name="mssqlserver_17194"></a>MSSQLSERVER_17194
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17194|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|伺服器無法載入登入所需的 SSL 提供者程式庫，此連接已經關閉。 SSL 可用來加密登入順序或所有通訊，視管理員對伺服器所做的設定而定。 請參閱線上叢書，以取得有關此錯誤訊息的資訊：0xXXXX。 [用戶端：11.11.11.11]|  
  
## <a name="explanation"></a>說明  
這個錯誤表示用戶端已經關閉連接。 發生這個錯誤是因為連接逾時期限已到。 錯誤訊息中顯示的值來自作業系統，提供基礎問題的說明。  
  
## <a name="user-action"></a>使用者動作  
如果訊息中的錯誤碼是 0x2746 (十進位值 10054)，即表示用戶端已經重設連接，通常是因為逾時之故。若要解決錯誤，請增加用戶端或呼叫端程式的連接逾時值。  
  
如需得知其他錯誤訊息值可行的解決方案，請使用作業系統命令 **net helpmsg** 並指定錯誤碼的十進位值。  
  
如需如何連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的詳細資訊，請參閱[伺服器網路組態](~/database-engine/configure-windows/server-network-configuration.md)和[用戶端網路組態](~/database-engine/configure-windows/client-network-configuration.md)。  
  
## <a name="internal-only"></a>僅供內部使用  
