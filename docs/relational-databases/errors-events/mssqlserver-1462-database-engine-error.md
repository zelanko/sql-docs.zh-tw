---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d53f3e8a00d0f93ac9c1738479cec05d2f01a602
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67908570"
---
# <a name="mssqlserver_1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
[疑難排解資料庫鏡像組態 &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
