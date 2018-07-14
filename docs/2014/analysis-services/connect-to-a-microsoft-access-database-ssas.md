---
title: 連接到 Microsoft Access 資料庫 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connaccessdb.f1
ms.assetid: 9fa81839-dd8b-41d3-915e-c774a707ed53
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c97b313a5f1cfc3a9c4dfb76f7f0b58f77e59f7b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37204458"
---
# <a name="connect-to-a-microsoft-access-database-ssas"></a>連接到 Microsoft Access 資料庫 (SSAS)
  [資料表匯入精靈] 的這個頁面可讓您指定連接到 Microsoft Access 資料庫的設定。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接 Microsoft Access 資料庫，您必須先在電腦上安裝適當的 ACE 提供者。 如需詳細資訊，請參閱[支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
> [!NOTE]  
>  在這個頁面中選取檔案時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選檔案讀取的權限，則匯入將不會成功。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **資料庫名稱**  
 為 Microsoft Access 資料庫檔案指定完整路徑。  
  
 **瀏覽**  
 導覽至可取得 Microsoft Access 資料庫檔案的位置。  
  
 **使用者名稱**  
 為資料庫連接指定使用者名稱。  
  
 **密碼**  
 為資料庫連接指定密碼。  
  
 **儲存我的密碼**  
 指定是否要儲存您在 **[密碼]** 方塊中輸入的密碼。  
  
 **進階**  
 使用 **[設定進階屬性]** 對話方塊設定其他連接屬性。  
  
 **測試連接**  
 嘗試使用目前的設定建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  
