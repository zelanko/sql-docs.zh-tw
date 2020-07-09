---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5a45061cc2618407f375150cda4afe744f491c4e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780470"
---
# <a name="mssqlserver_21899"></a>MSSQLSERVER_21899
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|21899|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21899|  
|訊息文字|在重新導向發行者 '%s' 上進行的查詢，可判斷原始發行者 '%s' 的訂閱者是否有 sysserver 項目失敗，發生錯誤 '%d'，錯誤訊息 '%s'。|  
  
## <a name="explanation"></a>說明  
**sp_validate_redirected_publisher** 會查詢位於遠端伺服器之發行者資料庫的訂閱中繼資料資料表，以便判斷其相關聯的訂閱者。 如果此查詢失敗，就會傳回錯誤 21899。 驗證查詢需要存取位於重新導向發行者的已發行資料庫。 針對原始發行者呼叫 **sp_adddistpublisher** 時，如果指定的登入未經授權，而無法存取位於重新導向發行者的已發行資料庫，就會傳回錯誤 21899。  
  
## <a name="user-action"></a>使用者動作  
請檢閱引用的錯誤訊息，以便判斷失敗的原因並且採取適當的更正動作。  
  
