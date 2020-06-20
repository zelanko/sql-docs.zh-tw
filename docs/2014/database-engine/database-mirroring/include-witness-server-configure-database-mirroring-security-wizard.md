---
title: 包含見證伺服器 (設定資料庫鏡像安全性精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.inclwitness.f1
ms.assetid: f04b38a4-f4e2-4d4c-bdac-7cc70e5a5684
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 57d476216b34053f6bb61deef719d082240ca0c8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934149"
---
# <a name="include-witness-server-configure-database-mirroring-security-wizard"></a>包含見證伺服器 (設定資料庫鏡像安全性精靈)
  使用此頁面，來指定您是否想要將見證伺服器包含在資料庫鏡像的這個安全性組態中。  
  
 **若要使用 SQL Server Management Studio 設定資料庫鏡像**  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [啟動設定資料庫鏡像安全性精靈 &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>選項。  
 **是**  
 按一下即可將見證伺服器執行個體包含在安全性組態中。 具有自動容錯移轉的高安全性模式必須要有見證伺服器，如果主體伺服器執行個體失敗，這個見證伺服器就可以支援自動容錯移轉至鏡像伺服器執行個體。  
  
 **否**  
 按一下即可設定不具見證的安全性。  
  
## <a name="see-also"></a>另請參閱  
 [[鏡像] 頁面 &#40;的資料庫屬性&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [資料庫鏡像見證](database-mirroring-witness.md)  
  
  
