---
title: 連接到 Microsoft Excel 檔案（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connexcelfile.f1
ms.assetid: 126f7d6b-d270-40e7-b23e-8d114f87065b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6646ee55ce6703391b5c146d41d513445aa2fabd
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527184"
---
# <a name="connect-to-a-microsoft-excel-file-ssas"></a>連接到 Microsoft Excel 檔案 (SSAS)
  **[資料表匯入精靈]** 的這個頁面可讓您連接到儲存在本機電腦上的 Microsoft Excel 檔案。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接 Microsoft Excel 檔案，您必須先在電腦上安裝適當的 ACE 提供者。 如需詳細資訊，請參閱[支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
> [!NOTE]  
>  在這個頁面中選取檔案時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選檔案讀取的權限，則匯入將不會成功。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **Excel 檔案路徑**  
 指定 Excel 檔案的完整路徑。  
  
 **瀏覽**  
 導覽至有 Excel 檔案可用的位置。  
  
 **進階**  
 使用 [**設定高級屬性**] 對話方塊來設定其他連接屬性。  
  
 **使用第一個資料列做為資料行標頭**  
 指定是否要使用第一個資料列做為目的地資料表的資料行標頭。  
  
 **測試連接**  
 嘗試使用目前的設定建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  
