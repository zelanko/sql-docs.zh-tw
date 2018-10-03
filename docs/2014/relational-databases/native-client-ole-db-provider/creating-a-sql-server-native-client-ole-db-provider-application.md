---
title: 建立 SQL Server Native Client OLE DB 提供者應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f2476ebb3997db16c8ffebdd0aac2d6eebe9a68
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182688"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>建立 SQL Server Native Client OLE DB 提供者應用程式
  建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者應用程式牽涉到以下步驟：  
  
1.  建立與資料來源的連接。  
  
2.  執行命令。  
  
3.  處理結果。  
  
> [!NOTE]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，則應該用 [Win32 cryptoAPI](http://go.microsoft.com/fwlink/?LinkId=9504) 加密這些認證。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立資料來源的連接](establishing-a-connection-to-a-data-source.md)  
  
-   [執行命令](executing-a-command.md)  
  
-   [處理結果](processing-results.md)  
  
-   [關於 OLE DB 屬性](about-ole-db-properties.md)  
  
-   [在 SQL Server Native Client 中使用 OUTPUT 子句搭配 OLE DB](using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
