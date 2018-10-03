---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ba40eba38d4659f100dd5aa9671e87f51b366b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758066"
---
# <a name="mssqlserver5554"></a>MSSQLSERVER_5554
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|MSSQLSERVER|  
|事件識別碼|5554|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|FS_MINIVER_OVERFLOW|  
|訊息文字|單一檔案的版本總數已到達檔案系統設定的上限。|  
  
## <a name="explanation"></a>說明  
在 Multiple Active Result Sets (MARS) 或觸發程序案例中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用作業系統所指定的迷你版本。  
  
## <a name="user-action"></a>使用者動作  
嘗試避免重複更新相同交易內的資料。  
  
