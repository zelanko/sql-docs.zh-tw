---
title: 連接到 Oracle Database （SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connoracledb.f1
ms.assetid: 9bd177fb-8539-46cd-bf96-189ade52c2a1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8bc5a08d96dbef0bae412b75c9592e4893e12a0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087015"
---
# <a name="connect-to-an-oracle-database-ssas"></a>連接到 Oracle 資料庫 (SSAS)
  
  **[資料表匯入精靈]** 的這個頁面可讓您指定連接到 Oracle 資料庫的設定。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至資料來源，您必須先在電腦上安裝適當的提供者。  
  
> [!NOTE]  
>  在這個頁面中選取資料庫時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選取資料庫讀取的權限，則匯入將不會成功。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **伺服器名稱**  
 輸入或選取要連接的伺服器執行個體名稱。  
  
 **使用者名稱**  
 為資料庫連接指定使用者名稱。  
  
 這個使用者名稱是在建構資料來源的連接字串時使用。 這些認證也會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **密碼**  
 為資料庫連接指定密碼。  
  
 **儲存我的密碼**  
 指定是否要儲存您在 **[密碼]** 方塊中輸入的密碼。  
  
 **進階**  
 使用 [**設定高級屬性**] 對話方塊來設定其他連接屬性。 如需詳細資訊，請參閱[設定進階屬性 &#40;SSAS&#41;](set-advanced-properties-ssas.md)。  
  
 **測試連接**  
 嘗試使用目前的設定建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  
