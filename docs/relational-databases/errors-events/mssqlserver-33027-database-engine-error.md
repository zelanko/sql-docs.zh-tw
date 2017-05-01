---
title: MSSQLSERVER_33027 | Microsoft Docs
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
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8d7e546f593d1a54c2787da74cfe34502598a0b3
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|33027|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_CRYPTOPROV_CANTLOADDLL|  
|訊息文字|無法載入密碼編譯提供者 '%.*ls'，因為 Authenticode 簽章或檔案路徑無效。 請檢查先前其他失敗的訊息。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法使用錯誤訊息中所列的密碼編譯提供者，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法載入 DLL。 此名稱無效，或者 Authenticode 簽章無效。  
  
## <a name="user-action"></a>使用者動作  
檢查檔案是否存在，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否擁有存取該位置的權限。 檢查其他相關訊息的錯誤記錄檔。 否則，如需詳細資訊，請連絡密碼編譯提供者。  
  

