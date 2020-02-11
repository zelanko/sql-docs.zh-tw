---
title: 命令列管理工具： SqlLocalDB .exe |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ea983555fdcb4bb177813db88d40f4bcc59c0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63128789"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>命令列管理工具：SqlLocalDB.exe
  SqlLocalDB.exe 是可讓使用者從命令列輕鬆管理 LocalDB 執行個體的簡單工具。 它會實作為 LocalDB 執行個體 API 外圍的簡單包裝函式。 就像在許多類似的 SQL Server 工具 (例如 SQLCMD) 中一樣，參數會當做命令列引數傳遞給 SqlLocalDB，並且將輸出傳送到主控台。  
  
 SqlLocalDB 可讓開發人員使用 LocalDB，而不需要撰寫呼叫 API 的程式碼，或依賴其他工具來完成作業。  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB 選項  
 SqlLocalDB 支援下列選項。  
  
|選項|作用|  
|------------|------------------|  
|`-?`|列印說明文字。|  
|`create&#124;c "instance name" [version-number] [-s]`|以指定的名稱和版本建立新的 LocalDB 執行個體。<br /><br /> 如果省略 [version-number] 參數，預設為 SqlLocalDB 組建版本。<br /><br /> -s 會啟動新建立的 LocalDB 執行個體。|  
|`delete&#124;d "instance name"`|刪除具有指定之名稱的 LocalDB 執行個體。|  
|`start&#124;s "instance name"`|啟動具有指定之名稱的 LocalDB 執行個體。|  
|`stop&#124;p "instance name" [-i&#124;-k]`|在目前查詢完成執行之後，停止具有指定之名稱的 LocalDB 執行個體。<br /><br /> -i 會使用 NOWAIT 選項要求關閉 LocalDB 執行個體。<br /><br /> -k 會在未經連絡的情況下終止 LocalDB 執行個體處理序。|  
|`share&#124;h ["owner SID or account"] "private name" "shared name"`|使用指定的共用名稱來共用指定的私用執行個體。 如果省略使用者 SID 或帳戶名稱，會預設為目前的使用者。|  
|`unshare&#124;u "shared name"`|取消共用指定的共用 LocalDB 執行個體。|  
|`info&#124;i`|列出目前使用者擁有之所有現有的 LocalDB 執行個體，以及所有共用的 LocalDB 執行個體。|  
|`info&#124;i "instance name"`|列印指定之 LocalDB 執行個體的相關資訊。|  
|`versions&#124;v`|列出電腦上安裝的所有 LocalDB 版本。|  
|||  
|`trace&#124;t on&#124;off`|開啟及關閉追蹤。|  
  
 SqlLocalDB 會將空格視為分隔符號；你必須使用引號括住包含空格和特殊字元的執行個體名稱。 例如：  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
