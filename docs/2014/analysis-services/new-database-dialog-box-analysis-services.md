---
title: 新增資料庫對話方塊 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.newdatabase.f1
ms.assetid: ddc7804b-acb0-4ae4-a88f-e8cdf704c341
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed652c47be4bfbe2783f5138bb80f8ed9c37dd32
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072310"
---
# <a name="new-database-dialog-box-analysis-services"></a>新增資料庫對話方塊 (Analysis Services)
  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [新增資料庫] 對話方塊，即可建立空的新 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。 在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的 [資料庫] 資料夾，然後選取 [新增資料庫]，即可顯示[新增資料庫] 對話方塊。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**資料庫名稱**|輸入新 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的名稱。|  
|**使用特定的使用者名稱和密碼**|選取即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫使用所指定使用者帳戶的安全性認證。 指定的認證將用於處理、ROLAP 查詢、非正規繫結、本機 Cube、採礦模型、遠端資料分割、連結物件以及從目標到來源的同步處理。 但是，DMX OPENQUERY 陳述式將使用目前使用者的認證。|  
|**使用者名稱**|輸入選取的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫所要使用之使用者帳戶的網域和名稱。 使用下列格式：<br /><br /> *\<網域名稱 >* **\\** *\<使用者帳戶名稱 >*<br /><br /> 注意:會啟用此選項，只有當**使用特定的使用者名稱和密碼**已選取。|  
|**密碼**|輸入 [使用者名稱] 中所指定之使用者帳戶的密碼。|  
|**使用服務帳戶**|選取即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫使用管理資料庫之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服務相關聯的安全性認證。 服務帳戶認證將用於處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理。 但是，DMX OPENQUERY 陳述式、本機 Cube 和採礦模型將使用目前使用者的認證。 非正規 (out-of-line) 繫結不支援此選項。|  
|**使用目前使用者的認證**|選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫使用目前使用者的安全性認證來進行非正規 (out-of-line) 繫結、DMX OPENQUERY 陳述式、本機 Cube 和採礦模型。 處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理不支援此選項。|  
|**預設值**|選取此選項即可使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]之預設使用者帳戶的認證。 此選項會使用資料庫的預設值來處理物件、同步處理伺服器和執行 **Open Query** 資料採礦陳述式。 如需指定在資料庫層級之預設設定的詳細資訊，請參閱[設定多維度資料庫屬性 &#40;Analysis Services&#41;](multidimensional-models/set-multidimensional-database-properties-analysis-services.md)。<br /><br /> 依預設`DataSourceImpersonationInfo`資料庫屬性設定為**使用的服務帳戶**。 不論 `DataSourceImpersonationInfo` 屬性值為何，目前使用者的認證都將用於非正規 (out-of-line) 繫結、ROLAP 查詢、本機 Cube 和資料採礦模型。|  
|**說明**|輸入新 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的描述。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型資料庫 &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
