---
title: 連接到 DB2 資料庫（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndb2db.f1
ms.assetid: eeef3697-a4fd-4263-ba7e-f86afa1f46cc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03c98f3ab44a4a9f3aac91be36f3d704a3f796ab
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527214"
---
# <a name="connect-to-a-db2-database-ssas"></a>連接到 DB2 資料庫 (SSAS)
  [資料表匯入精靈]**** 的這個頁面可讓您指定連接到 DB2 資料庫的設定。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至資料來源，您必須先在電腦上安裝適當的提供者。  
  
> [!NOTE]  
>  在這個頁面中選取資料庫時，會使用所指定使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選取資料庫讀取的權限，則匯入將不會成功。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **伺服器名稱**  
 輸入或選取要連接的伺服器執行個體。  
  
 **使用者名稱**  
 為資料庫連接指定使用者名稱。  
  
 這個使用者名稱是在建構資料來源的連接字串時使用。 這些認證也會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **密碼**  
 為資料庫連接指定密碼。  
  
 **儲存我的密碼**  
 指定是否要儲存您在 **[密碼]** 方塊中輸入的密碼。  
  
 **資料庫名稱**  
 從資料庫清單中選取資料庫。  
  
 **封裝集合**  
 指定 DB2 封裝集合的名稱。 提供者會使用封裝來發出 SQL 陳述式及呼叫預存程序。  
  
 **預設結構描述**  
 為選取的資料庫指定預設結構描述名稱。  
  
 **進階**  
 使用 [**設定高級屬性**] 對話方塊來設定其他連接屬性。  
  
 **測試連接**  
 嘗試使用目前的設定建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  
