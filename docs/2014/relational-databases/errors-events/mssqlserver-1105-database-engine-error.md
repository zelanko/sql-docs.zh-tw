---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a82ae33f7e05ef2539b358d4b60ac8ecced38c74
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968038"
---
# <a name="mssqlserver_1105"></a>MSSQLSERVER_1105
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1105|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NO_MORE_SPACE_IN_FG|  
|訊息文字|檔案群組已滿，無法在資料庫中為物件 '%.*ls'%.\*ls 配置空間，檔案群組：'%.\*ls'，資料庫：'%.\*ls'。 請刪除不必要的檔案、卸除檔案群組中的物件、將其他檔案加入檔案群組，或者將檔案群組中現有的檔案設定為自動成長，以產生磁碟空間。|  
  
## <a name="explanation"></a>說明  
 檔案群組中沒有可用的磁碟空間。  
  
## <a name="user-action"></a>使用者動作  
 下列動作可以在檔案群組中提供可用的空間：  
  
-   開啟自動成長功能。  
  
-   加入更多檔案到檔案中。  
  
-   卸除已經不需要的索引或資料表，以釋出磁碟空間。  
  
-   如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜資料磁碟空間不足的疑難排解＞。  
  
> [!NOTE]  
>  當索引位於數個檔案時，則當其中一個檔案已滿時，`ALTER INDEX REORGANIZE` 會傳回錯誤 1105。 當程序嘗試將列移至已滿的檔案時，會封鎖此重組的程序。 若要解決此限制，請執行 `ALTER INDEX REBUILD` 而不是 `ALTER INDEX REORGANIZE`，或是為已滿的檔案增加檔案成長限制。  
  
  
