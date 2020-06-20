---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7e356b3de7ce46ae64d2d94461eed16b2d36baa6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034430"
---
# <a name="mssqlserver_2516"></a>MSSQLSERVER_2516
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2516|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|訊息文字|修復導致資料庫 NAME 的差異式點陣圖無效。 差異備份鏈已中斷。 您必須執行完整的資料庫備份，然後才能執行差異備份。|  
  
## <a name="explanation"></a>說明  
 在修復錯誤 MSSQLEngine_2515 時，會傳回這項參考用訊息。  
  
## <a name="user-action"></a>使用者動作  
 執行完整的資料庫備份。  
  
## <a name="see-also"></a>另請參閱  
 [建立完整資料庫備份 &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
  
