---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edebfb36a1693f2a7d6a94d7c006d80e2bb27683
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62914621"
---
# <a name="mssqlserver_26014"></a>MSSQLSERVER_26014
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
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
  
  
