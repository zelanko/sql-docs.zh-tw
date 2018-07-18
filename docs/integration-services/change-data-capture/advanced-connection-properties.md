---
title: 進階連線屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 47635a9cfc4c14f3420d342fdb707d6ae916c78f
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35405590"
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
 [存取 CDC 設計工具主控台](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [用來建立執行個體的 SQL Server 連接](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
