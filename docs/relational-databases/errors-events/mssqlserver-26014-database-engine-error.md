---
description: MSSQLSERVER_26014
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9bb0b7deb6927cf319083a63c789fc1fbf07a26f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424460"
---
# <a name="mssqlserver_26014"></a>MSSQLSERVER_26014
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|26014|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SNI_SSL_USER_CERT_FAILURE|  
|訊息文字|無法載入使用者指定的憑證 [Cert Hash(sha1) "%hs"]。 伺服器將不會接受連接。 您應該確認已正確安裝憑證。 請參閱線上叢書中的＜設定憑證給 SSL 使用＞(Configuring Certificate for Use by SSL)。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已嘗試載入在訊息中指定的憑證，但是作業失敗。 您必須先解決此問題，然後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 才能使用這個憑證。  
  
造成此錯誤的可能原因包括：  
  
-   憑證可能已經移動或刪除。  
  
-   如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的登入已經變更，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能就沒有存取此憑證的權限。  
  
-   憑證可能已經過期。  
  
## <a name="user-action"></a>使用者動作  
請確定在訊息中指定的憑證存在系統上、可以存取，而且可供使用。  
  
