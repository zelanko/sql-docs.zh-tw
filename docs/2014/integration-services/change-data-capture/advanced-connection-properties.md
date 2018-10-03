---
title: 進階連線屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5a621cc9377f20b5f184f76258f0bc5208dfe7c2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48195868"
---
# <a name="advanced-connection-properties"></a>進階連接屬性
  使用 **[進階連接屬性]** 對話方塊可在連接字串中加入其他連接參數。  
  
 其他連接參數可以是您使用之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行個體所支援的任何 ODBC 連接參數。  
  
 您使用 **[進階連接屬性]** 對話方塊所加入的參數會加入至 **[連接到 SQL Server]** 對話方塊中所選取的參數。  
  
 提供之每一個參數的最後一個執行個體都會覆寫該參數之前的任何執行個體。 使用 **[進階連接參數]** 對話方塊加入的參數會遵循及取代 **[SQL Server 連接]** 對話方塊中所提供的參數。 例如，如果 [SQL Server 連接] 對話方塊指定 SERVER1 當做伺服器名稱，而且 [其他連接參數] 頁面包含 ;SERVER=SERVER2，則會對 SERVER2 進行連接。  
  
 使用 **[進階連接屬性]** 對話方塊加入的參數會以純文字格式傳遞。  
  
> [!IMPORTANT]  
>  請勿在 **[進階連接屬性]** 對話方塊中包含登入認證。 當透過網路傳遞認證和密碼時，將不會加密。  
  
## <a name="see-also"></a>另請參閱  
 [存取 CDC 設計工具主控台](access-the-cdc-designer-console.md)   
 [用來建立執行個體的 SQL Server 連接](sql-server-connection-for-instance-creation.md)  
  
  
