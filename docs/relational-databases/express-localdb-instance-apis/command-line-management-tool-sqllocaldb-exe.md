---
title: "命令列管理工具： SqlLocalDB.exe |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apilocation: sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8f2bac1f105f5d299fa97d11fa579226026134aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>命令列管理工具：SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SqlLocalDB.exe 是一個簡單工具，可讓使用者輕鬆地從命令列管理 LocalDB 執行個體。 它會實作為 LocalDB 執行個體 API 外圍的簡單包裝函式。 就像在許多類似的 SQL Server 工具 (例如 SQLCMD) 中一樣，參數會當做命令列引數傳遞給 SqlLocalDB，並且將輸出傳送到主控台。  
  
 SqlLocalDB 可讓開發人員使用 LocalDB，而不需要撰寫呼叫 API 的程式碼，或依賴其他工具來完成作業。  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB 選項  
 SqlLocalDB 支援下列選項。  
  
|選項|用途|  
|------------|------------------|  
|`-?`|列印說明文字。|  
|' create\|c 「 執行個體名稱 」 version-number] [-s]'|以指定的名稱和版本建立新的 LocalDB 執行個體。<br /><br /> 如果省略 [version-number] 參數，預設為 SqlLocalDB 組建版本。<br /><br /> -s 會啟動新建立的 LocalDB 執行個體。|  
|' delete\|「 執行個體名稱 」 d'|刪除具有指定之名稱的 LocalDB 執行個體。|  
|' 才能執行|「 執行個體名稱 」 s'|啟動具有指定之名稱的 LocalDB 執行個體。|  
|' stop\|p [執行個體名稱] [-i\|-k]'|在目前查詢完成執行之後，停止具有指定之名稱的 LocalDB 執行個體。<br /><br /> -i 會使用 NOWAIT 選項要求關閉 LocalDB 執行個體。<br /><br /> -k 會在未經連絡的情況下終止 LocalDB 執行個體處理序。|  
|' share\|h [「 擁有者 SID 或帳戶 」] 「 私用名稱 」 「 共用的名稱 」 '|使用指定的共用名稱來共用指定的私用執行個體。 如果省略使用者 SID 或帳戶名稱，會預設為目前的使用者。|  
|' unshare\|u [共用的名稱] '|取消共用指定的共用 LocalDB 執行個體。|  
|' info\|我 '|列出目前使用者擁有之所有現有的 LocalDB 執行個體，以及所有共用的 LocalDB 執行個體。|  
|' info\|「 執行個體名稱 」 i'|列印指定之 LocalDB 執行個體的相關資訊。|  
|' versions\|v'|列出電腦上安裝的所有 LocalDB 版本。|  
|||  
|' trace\|t 可依|關閉 '|開啟及關閉追蹤。|  
  
 SqlLocalDB 會將空格視為分隔符號；你必須使用引號括住包含空格和特殊字元的執行個體名稱。 例如：  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
