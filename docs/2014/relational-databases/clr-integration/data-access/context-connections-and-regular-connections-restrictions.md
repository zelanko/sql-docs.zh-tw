---
title: 一般和內容連接的限制 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f0d266b75dad229a0784606af112c249728a112c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135170"
---
# <a name="restrictions-on-regular-and-context-connections"></a>一般和內容連接的限制
  本主題討論中執行程式碼的相關限制[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]透過內容和一般連接處理序。  
  
## <a name="restrictions-on-context-connections"></a>內容連接的限制  
 開發應用程式時，請考慮下列適用於內容連接的限制：  
  
-   在給定連接的給定時間內，您只能開啟一個內容連接。 如果您同時在不同的連接中執行多個陳述式，其中每個陳述式可能會取得自己的內容連接。 這項限制不會影響來自不同連接的並行要求，只會影響給定連接的給定要求。  
  
-   內容連接不支援 Multiple Active Result Sets (MARS)。  
  
-   `SqlBulkCopy` 類別無法在內容連接中運作。  
  
-   不支援在內容連接中更新批次。  
  
-   `SqlNotificationRequest` 無法搭配針對內容連接執行的命令使用。  
  
-   不支援取消針對內容連接執行的命令。 `SqlCommand.Cancel` 方法會以無訊息的方式忽略此要求。  
  
-   當您使用 "context connection=true" 時，無法使用其他連接字串關鍵字。  
  
-   如果 `SqlConnection.DataSource` 的連接字串為 "context connection=true"，`SqlConnection` 屬性就會傳回 Null，而非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
-   針對內容連接執行命令時，設定 `SqlCommand.CommandTimeout` 屬性就沒有任何作用。  
  
## <a name="restrictions-on-regular-connections"></a>一般連接的限制  
 開發應用程式時，請考慮下列適用於一般連接的限制：  
  
-   不支援針對內部伺服器執行非同步命令。 如果您在命令的連接字串中包含 "async=true"，然後執行此命令，就會導致系統擲回 `System.NotSupportedException`。 此訊息會顯示：「在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 處理序內部執行時，不支援非同步處理」。  
  
-   不支援 `SqlDependency` 物件。  
  
## <a name="see-also"></a>另請參閱  
 [內容連接](context-connection.md)  
  
  