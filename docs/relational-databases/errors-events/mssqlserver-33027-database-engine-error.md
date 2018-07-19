---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d9b03347fb6ca83827854f4af0b75e8accc131
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190948"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|33027|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_CRYPTOPROV_CANTLOADDLL|  
|訊息文字|無法載入密碼編譯提供者 '%.*ls'，因為 Authenticode 簽章或檔案路徑無效。 請檢查先前其他失敗的訊息。|  
  
## <a name="explanation"></a>說明  
SQL Server 無法使用錯誤訊息中所列的密碼編譯提供者，因為 SQL Server 無法載入 DLL。 此名稱無效，或者 Authenticode 簽章無效。  
  
## <a name="user-action"></a>使用者動作  
檢查檔案是否存在，而且 SQL Server 是否擁有存取該位置的權限。 檢查其他相關訊息的錯誤記錄檔。 否則，如需詳細資訊，請連絡密碼編譯提供者。  
  
