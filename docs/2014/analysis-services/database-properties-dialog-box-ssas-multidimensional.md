---
title: 資料庫屬性對話方塊 (SSAS-多維度) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.databaseproperties.f1
ms.assetid: 70f000b7-917f-4699-b142-7a0d13ff767c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be4133aa143ecf0e1fb9b50c40a38a73b4207f30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082315"
---
# <a name="database-properties-dialog-box-ssas---multidimensional"></a>資料庫屬性對話方塊 (SSAS - 多維度)
  使用 **中的** [資料庫屬性] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 對話方塊，即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中之資料庫的屬性。 您可以在 [物件總管] 中以滑鼠右鍵按一下資料庫，然後選取 [屬性]  ，藉以顯示 [資料庫屬性]  對話方塊。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱**|輸入以變更資料庫的名稱。|  
|**ID**|顯示資料庫的識別碼。|  
|**說明**|鍵入以變更資料庫的描述。|  
|**建立時間戳記**|顯示建立資料庫的日期和時間。|  
|**上次結構描述更新**|顯示上次更新資料庫的中繼資料的日期和時間。|  
|**上次更新**|顯示上次更新資料庫之資料的日期和時間。|  
|**資料來源模擬資訊**|與資料庫中的資料來源進行連接和互動時，請選取資料庫使用的模擬資訊。 有效值包括以下的值：<br /><br /> **ImpersonateAccount** (使用特定的 Windows 使用者名稱和密碼)。<br /><br /> **ImpersonateService** (使用服務帳戶)。<br /><br /> **ImpersonateCurrentUser** (使用目前使用者的認證)。<br /><br /> **預設值** (使用服務帳戶進行 MOLAP 作業，而使用目前使用者進行資料採礦)。<br /><br /> 雖然您可以在資料庫層級進行資料來源模擬設定，不過這樣做只會影響針對其模擬設定指定 **[繼承]** 的這些資料來源。 直接針對資料來源指定的模擬設定一定會覆寫在資料庫層級指定的任何設定。<br /><br /> 選擇模擬選項時，請考慮需要系統支援的作業類型。 某些作業 (例如處理) 無法執行|  
|**上次處理**|顯示上次處理資料庫的日期和時間。|  
|**估計的大小**|顯示資料庫之估計的大小。|  
|**儲存體位置**|指定資料庫的位置。 如果資料庫位於預設資料目錄中，此值為空白。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型資料庫 &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
