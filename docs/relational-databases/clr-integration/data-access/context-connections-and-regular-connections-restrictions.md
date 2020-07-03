---
title: 一般和內容連接的限制 |Microsoft Docs
description: 本文描述透過內容和一般連接在 Microsoft SQL Server 程式中執行之程式碼的相關限制。
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
ms.openlocfilehash: 17f95da5b152dd73939dcdf8552f72c20f199f20
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882194"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>內容連線和一般連線 - 限制
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  本主題討論 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 透過內容和一般連接在進程中執行之程式碼的相關限制。  
  
## <a name="restrictions-on-context-connections"></a>內容連接的限制  
 開發應用程式時，請考慮下列適用於內容連接的限制：  
  
-   在給定連接的給定時間內，您只能開啟一個內容連接。 如果您同時在不同的連接中執行多個陳述式，其中每個陳述式可能會取得自己的內容連接。 這項限制不會影響來自不同連接的並行要求，只會影響給定連接的給定要求。  
  
-   內容連接不支援 Multiple Active Result Sets (MARS)。  
  
-   **SqlBulkCopy**類別不會在內容連接中運作。  
  
-   不支援在內容連接中更新批次。  
  
-   **SqlNotificationRequest**不能與針對內容連接執行的命令搭配使用。  
  
-   不支援取消針對內容連接執行的命令。 **SqlCommand. Cancel**方法會以無訊息方式忽略要求。  
  
-   當您使用 "context connection=true" 時，無法使用其他連接字串關鍵字。  
  
-   如果**sqlconnection**的連接字串為 "coNtext connection = true"，而不是實例的名稱，則**sqlconnection**屬性會傳回 null [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
-   在針對內容連接執行命令時，設定**CommandTimeout**屬性沒有作用。  
  
## <a name="restrictions-on-regular-connections"></a>一般連接的限制  
 開發應用程式時，請考慮下列適用於一般連接的限制：  
  
-   不支援針對內部伺服器執行非同步命令。 在命令的連接字串中包含 "async = true"，然後執行命令，會導致擲回**NotSupportedException** 。 此訊息會顯示：「在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 處理序內部執行時，不支援非同步處理」。  
  
-   不支援**SqlDependency**物件。  
  
## <a name="see-also"></a>另請參閱  
 [內容連接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
