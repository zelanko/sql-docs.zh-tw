---
title: Filestream 存取層級伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8335f821e2bd4026c17b0054e047125a0afd0177
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68011700"
---
# <a name="filestream-access-level-server-configuration-option"></a>檔案資料流存取層級伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  您可以使用 filestream_access_level 選項來變更這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的 FILESTREAM 存取層級。  
  
> [!NOTE]  
>  您必須先針對 FILESTREAM 啟用 Windows 管理設定，然後這個選項才會生效。 當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員時，可以啟用這些設定。  
  
|值|定義|  
|-----------|----------------|  
|0|針對這個執行個體停用 FILESTREAM 支援。|  
|1|針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取啟用 FILESTREAM。|  
|2|針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Win32 資料流存取啟用 FILESTREAM。|  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 組態 - Filestream](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [啟用及設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
