---
title: 開啟物件伺服器組態選項 | Microsoft Docs
description: 了解已停用的 [開啟物件] 組態選項。 查看 SQL Server 現在如何管理開啟資料庫物件的數目。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- open objects option
ms.assetid: c8424d3c-86ba-4cc5-bf0c-be4ce44bdd04
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0bbcb11a80f06eae10e5481c965e9216cc84695e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773626"
---
# <a name="open-objects-server-configuration-option"></a>開啟物件伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  雖然在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已停用此選項的功能，但此選項仍存在於 **sp_configure** 中。 (此設定無效)。在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，已開啟之資料庫物件的數目會受到動態管理，而且只受可用記憶體的限制。 **open objects** 選項可在 **sp_configure** 中使用，以保有與現有指令碼之間的回溯相容性。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
