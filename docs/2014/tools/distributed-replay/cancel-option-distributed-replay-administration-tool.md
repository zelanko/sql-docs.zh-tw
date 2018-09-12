---
title: 取消選項 (Distributed Replay 管理工具) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a231dc047362e3eb25342ae9b2d10cdbd0ee390
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820534"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>取消選項 (Distributed Replay 管理工具)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具， `DReplay.exe`，是命令列工具，可用來與 distributed 的 replay controller 通訊。 此主題描述 **cancel** 命令列選項與對應的語法。  
  
 **cancel** 選項會取消目前正在控制器上執行的作業。  
  
 ![主題連結圖示](../../database-engine/media/topic-link.gif "主題連結圖示") 如需管理工具語法所使用之語法慣例的詳細資訊，請參閱 [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)。  
  
## <a name="syntax"></a>語法  
  
```  
  
dreplay cancel [-mcontroller] [-q]   
```  
  
#### <a name="parameters"></a>參數  
 **-m** *controller*  
 控制器的電腦名稱。 您可以使用 "`localhost`" 或 "`.`" 表示本機電腦。  
  
 如果未指定 **-m** 參數，則會使用本機電腦。  
  
 **-q**  
 無訊息模式。 不會提示確認。  
  
 **-q** 參數是選用的。  
  
## <a name="examples"></a>範例  
 在下列範例中，會以無訊息模式提交取消要求。 `localhost` 值指出控制器服務與管理工具在同一部電腦上執行。  
  
```  
dreplay cancel –m localhost -q  
```  
  
## <a name="permissions"></a>Permissions  
 您必須以互動使用者、本機使用者或網域使用者帳戶來執行管理工具。 若要使用本機使用者帳戶，管理工具和控制器必須在同一部電腦上執行。  
  
 如需詳細資訊，請參閱 [Distributed Replay 安全性](distributed-replay-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)  
  
  
