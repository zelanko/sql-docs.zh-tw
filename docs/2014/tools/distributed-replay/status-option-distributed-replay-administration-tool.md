---
title: 狀態選項 (Distributed Replay 管理工具) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ce3d07bc357c5f3788fb6f995a43399021b3553
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048448"
---
# <a name="status-option-distributed-replay-administration-tool"></a>狀態選項 (Distributed Replay 管理工具)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 `DReplay.exe` 是命令列工具，可讓您用來與 Distributed Replay controller 通訊。 此主題描述 **status** 命令列選項與對應的語法。

 **status** 選項會查詢控制器，並顯示目前的狀態。

 ![主題連結圖示](../../database-engine/media/topic-link.gif "主題連結圖示") 如需搭配系統管理工具語法使用的語法慣例詳細資訊，請參閱 [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)。

## <a name="syntax"></a>語法

```

dreplay status [-mcontroller] [-fstatus_interval]
```

#### <a name="parameters"></a>參數
 **-m** *控制器*指定控制器的電腦名稱稱。 您可以使用 "`localhost`" 或 "`.`" 表示本機電腦。

 如果未指定 **-m** 參數，則會使用本機電腦。

 **-f** *status_interval*指定顯示狀態的頻率（以秒為單位）。

 如果未指定 **-f** 參數，預設間隔為 30 秒。

## <a name="examples"></a>範例
 在下列範例中，每隔 60 秒顯示目前狀態。 `localhost` 值指出控制器服務與管理工具在同一部電腦上執行。

```
dreplay status -m localhost -f 60
```

## <a name="permissions"></a>權限
 您必須以互動使用者、本機使用者或網域使用者帳戶來執行管理工具。 若要使用本機使用者帳戶，管理工具和控制器必須在同一部電腦上執行。

 如需詳細資訊，請參閱 [Distributed Replay 安全性](distributed-replay-security.md)。

## <a name="see-also"></a>另請參閱
 [SQL Server Distributed Replay](sql-server-distributed-replay.md) [transact-sql 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)


