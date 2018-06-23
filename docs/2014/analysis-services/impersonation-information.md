---
title: 模擬資訊 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 90a9d2102df9bd1b6cdf2bf1e4c7b3386c0fa825
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030687"
---
# <a name="impersonation-information"></a>模擬資訊
  使用 **[模擬資訊]** 頁面可指定 Analysis Services 將用來連接資料來源的認證。  
  
## <a name="options"></a>選項。  
 **使用特定的 Windows 使用者名稱和密碼**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用指定之 Windows 使用者帳戶的安全性認證。 指定的認證將用於處理、ROLAP 查詢、非正規繫結、本機 Cube、採礦模型、遠端資料分割、連結物件以及從目標到來源的同步處理。 但如果是資料採礦延伸模組 (DMX) OPENQUERY 陳述式，將忽略這個選項，而且會使用目前使用者的認證。  
  
 **使用者名稱**  
 輸入選定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件所要使用之使用者帳戶的網域和名稱。 使用下列格式：  
  
 *\<網域名稱 >* **\\** *\<使用者帳戶名稱 >*  
  
 唯有選取 **[使用特定的使用者名稱和密碼]** 之後，才會啟用此選項。  
  
 **密碼**  
 輸入選定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件所要使用之使用者帳戶的密碼。  
  
 唯有選取 **[使用特定的使用者名稱和密碼]** 之後，才會啟用此選項。  
  
 **使用服務帳戶**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用與管理該物件之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服務相關聯的安全性認證。 服務帳戶認證將用於處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理。 但如果是資料採礦延伸模組 (DMX) OPENQUERY 陳述式、本機 Cube 和採礦模型，將會使用目前使用者的認證。 非正規 (out-of-line) 繫結不支援此選項。  
  
 **使用目前使用者的認證**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用目前使用者的安全性認證來進行非正規 (out-of-line) 繫結、DMX OPENQUERY、本機 Cube 和採礦模型。 處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理不支援此選項。  
  
 **繼承**  
 選取此選項可使用定義於資料庫層級的模擬行為，伺服器管理員已經使用 `DataSourceImpersonation` 資料庫屬性來設定此行為。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支援的資料來源&#40;SSAS 多維度&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  