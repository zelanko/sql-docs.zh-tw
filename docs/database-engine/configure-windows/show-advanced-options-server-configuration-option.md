---
title: 顯示進階選項伺服器組態選項 | Microsoft Docs
description: 了解 [顯示進階選項] 選項。 了解如何使用此選項來在執行 SQL Server 系統預存程序 "sp_configure" 時列出進階選項。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sp_configure
- show advanced options option
ms.assetid: 7572372a-24b6-428f-84ae-48560430b159
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 77fb685deedf582f16c804ed2d8591383f6e9503
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751176"
---
# <a name="show-advanced-options-server-configuration-option"></a>顯示進階選項伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **show advanced options** 選項可用來顯示 **sp_configure** 系統預存程序進階選項。 若將 **show advanced options** 設成 1，就可以使用 **sp_configure**列出進階選項。 預設值是 0。  
  
 設定會立即生效，伺服器不必重新啟動。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
