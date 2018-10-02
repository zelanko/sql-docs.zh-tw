---
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
manager: craigg
ms.openlocfilehash: 3de21bc77c9840cd4604ee178c95cac1711c251c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740036"
---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
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
  
