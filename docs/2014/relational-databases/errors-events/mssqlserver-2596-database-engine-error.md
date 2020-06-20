---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27b2ceed40274df4ba57c4d61a83fbc60b6a7f80
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034048"
---
# <a name="mssqlserver_2596"></a>MSSQLSERVER_2596
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2596|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|訊息文字|未處理修復陳述式。 資料庫不可以是唯讀模式。|  
  
## <a name="explanation"></a>說明  
 此訊息指出資料庫為唯讀模式。 當資料庫處於唯讀模式時，便無法進行修復。  
  
## <a name="user-action"></a>使用者動作  
 使用 ALTER DATABASE 將資料庫設定成讀取/寫入，然後重新執行 DBCC 命令。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
