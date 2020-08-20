---
description: MSSQLSERVER_33027
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce43e69dd5b90b72c84d49c41387896c4b664a60
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476033"
---
# <a name="mssqlserver_33027"></a>MSSQLSERVER_33027
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|33027|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_CRYPTOPROV_CANTLOADDLL|  
|訊息文字|無法載入密碼編譯提供者 '%.*ls'，因為 Authenticode 簽章或檔案路徑無效。 請檢查先前其他失敗的訊息。|  
  
## <a name="explanation"></a>說明  
SQL Server 無法使用錯誤訊息中所列的密碼編譯提供者，因為 SQL Server 無法載入 DLL。 此名稱無效，或者 Authenticode 簽章無效。  
  
## <a name="user-action"></a>使用者動作  
檢查檔案是否存在，而且 SQL Server 是否擁有存取該位置的權限。 檢查其他相關訊息的錯誤記錄檔。 否則，如需詳細資訊，請連絡密碼編譯提供者。  
  
