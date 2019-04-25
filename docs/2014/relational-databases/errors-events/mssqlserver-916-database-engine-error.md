---
title: MSSQLSERVER_916 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aeeda48970696fa3d2f1da22f9aa318910bd53dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761757"
---
# <a name="mssqlserver916"></a>MSSQLSERVER_916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|916|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NOTUSER|  
|訊息文字|伺服器主體 "%.*ls" 在目前的安全性內容下無法存取資料庫 "%.\*ls"。|  
  
## <a name="explanation"></a>說明  
登入沒有足夠的權限來連接至具名資料庫。 可以連接至這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體但在資料庫中沒有特定權限的登入會接收 guest 使用者的權限。 此安全措施可以避免某資料庫的使用者無法連接其無權存取的資料庫。 當 guest 使用者沒有具名資料庫的 CONNECT 權限，也沒有設定可信任的屬性時，即可能會出現此錯誤訊息。 當 guest 使用者沒有具名資料庫的 CONNECT 權限時，可能就會出現這個錯誤訊息。  
  
當 msdb 資料庫的 CONNECT 權限遭到拒絕或撤銷時，如果 [物件總管] 嘗試顯示每個資料庫的以原則為基礎的管理狀態，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可能會收到這個錯誤。 [物件總管] 會使用目前登入的權限，在 msdb 資料庫中查詢這項資訊，因而導致錯誤發生。 此外，系統也會出現下列錯誤訊息：  
  
無法擷取此要求的資料。 (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>使用者動作  
  
> [!WARNING]  
> 只要確實了解使用者在不同資料庫是否皆能通過驗證，即可避開此安全性措施。 下列幾種方法可能會允許具有某資料庫權限的使用者，連接其他可能會將資料公開給惡意使用者的資料庫。 在啟用自主資料庫時，以下步驟可讓某資料庫的資料庫擁有者授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上其他資料庫的存取權。  
  
您可以透過下列其中一種方式連接資料庫：  
  
-   將具名資料庫的存取權授與特定的登入。 下列範例會將 `Adventure-Works\Larry` 資料庫的存取權授與 `msdb` 登入。  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO [Adventure-Works\Larry] ;  
  
-   將錯誤訊息中指定之資料庫的 CONNECT 權限授與 guest 使用者。 下列範例會將 `CONNECT` 資料庫的 `msdb` 權限授與 `guest` 使用者。  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO guest ;  
  
-   啟用已經驗證使用者之資料庫的 TRUSTWORTHY 屬性。  
  
    `ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;`  
  
