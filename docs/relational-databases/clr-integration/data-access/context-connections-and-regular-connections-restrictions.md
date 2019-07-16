---
title: 一般和內容連接的限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: d8cbdd195f698090602b98cdb6e5bab0a86556ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216416"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>內容連線和一般連線 - 限制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題討論與執行中的程式碼相關聯的限制[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]透過內容和一般連接處理序。  
  
## <a name="restrictions-on-context-connections"></a>內容連接的限制  
 開發應用程式時，請考慮下列適用於內容連接的限制：  
  
-   在給定連接的給定時間內，您只能開啟一個內容連接。 如果您同時在不同的連接中執行多個陳述式，其中每個陳述式可能會取得自己的內容連接。 這項限制不會影響來自不同連接的並行要求，只會影響給定連接的給定要求。  
  
-   內容連接不支援 Multiple Active Result Sets (MARS)。  
  
-   **SqlBulkCopy**類別內容連接中無法運作。  
  
-   不支援在內容連接中更新批次。  
  
-   **SqlNotificationRequest**無法搭配針對內容連接執行的命令。  
  
-   不支援取消針對內容連接執行的命令。 **SqlCommand.Cancel**方法會以無訊息方式忽略要求。  
  
-   當您使用 "context connection=true" 時，無法使用其他連接字串關鍵字。  
  
-   **SqlConnection.DataSource**屬性會傳回 null 值的連接字串如果**SqlConnection**是 「 內容連線 = true"，而不是執行個體名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   設定**SqlCommand.CommandTimeout**屬性沒有任何作用，針對內容連接執行命令。  
  
## <a name="restrictions-on-regular-connections"></a>一般連接的限制  
 開發應用程式時，請考慮下列適用於一般連接的限制：  
  
-   不支援針對內部伺服器執行非同步命令。 包括"async = true 」 在連接字串的命令，然後再執行命令，會導致**System.NotSupportedException**所擲回。 此時會出現此訊息：「 在執行時不支援非同步處理[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]程序。 」  
  
-   **SqlDependency**不支援物件。  
  
## <a name="see-also"></a>另請參閱  
 [內容連接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
