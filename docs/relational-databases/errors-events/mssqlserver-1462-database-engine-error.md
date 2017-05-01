---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 354280b813e73ec3090ae3c5ce5459eb008191d3
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1462|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|訊息文字|重做作業失敗，已停用資料庫鏡像。 無法繼續。|  
  
## <a name="explanation"></a>說明  
資料庫鏡像無法在鏡像上重做記錄。  
  
### <a name="possible-causes"></a>可能的原因  
在主體資料庫上執行加入檔案作業成功，但接著在鏡像資料庫上執行卻失敗，最可能的原因是主體伺服器與鏡像伺服器上的檔案名稱或目錄結構不同的緣故。  
  
## <a name="user-action"></a>使用者動作  
查詢 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，找出造成這個錯誤的原因。 嘗試解決失敗的原因，然後在資料庫上繼續執行鏡像。  
  
## <a name="see-also"></a>另請參閱  
[為資料庫鏡像組態疑難排解 &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  

