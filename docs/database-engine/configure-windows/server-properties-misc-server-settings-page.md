---
title: 伺服器屬性 (其他伺服器設定頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.miscserversettings.f1
ms.assetid: b170c066-30cd-42dd-8d34-aa129ea09551
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 62a8af2e4a82a0a0bdeec231db62c2166ed030de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030836"
---
# <a name="server-properties---misc-server-settings-page"></a>伺服器屬性 - 其他伺服器設定頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此頁面來檢視或修改伺服器設定。  
  
## <a name="options"></a>選項。  
 **使用者的預設語言**  
 指定所有新建立之登入的預設語言。  
  
 **允許觸發程序引發其他觸發程序**  
 控制觸發程序是否可以執行起始另一個觸發程序的動作。 清除此選項時，無法由另一個觸發程序來引發觸發程序。 選取此選項時，可以由另一個觸發程序來引發觸發程序，最多可達 32 個層級。  
  
 **使用查詢管理員防止長期執行的查詢**  
 指定可在其中執行查詢的時間上限。 查詢成本代表在特定的硬體組態上，預估執行查詢所需的時間 (以秒為單位)。 依預設，查詢管理員會關閉而允許執行所有查詢。 如果選取此選項，您必須在下面文字方塊中輸入時間限制。 如果指定非零的非負值，查詢若超過該值的估計成本，查詢管理員就不允許執行此查詢。  
  
 **將兩位數年份解譯為介於**  
 指定用於解譯兩位數年份值的 100 年日期範圍。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將參考指定範圍的年份，來解譯兩位數日期值。  
  
 以結束年份設定右邊的方塊。 儲存結束年份時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將自動使用開始年份來擴展左邊的方塊。  
  
 **設定的值**  
 針對此窗格中的選項，顯示設定的值。 如果您變更這些值，請按一下 **[執行中的值]** ，即可查看變更是否已生效。 如果變更尚未生效，必須先重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 **[執行中的值]**  
 針對此窗格中的選項，檢視目前執行中的值。 這些值是唯讀的。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
