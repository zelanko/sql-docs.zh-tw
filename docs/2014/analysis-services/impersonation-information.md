---
title: 模擬資訊 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
author: minewiskan
ms.author: owend
ms.openlocfilehash: bd1a2952c54974d924fdeca23d3173a690579d2b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544240"
---
# <a name="impersonation-information"></a>模擬資訊
  使用 **[模擬資訊]** 頁面可指定 Analysis Services 將用來連接資料來源的認證。  
  
## <a name="options"></a>選項  
 **使用特定的 Windows 使用者名稱和密碼**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用指定之 Windows 使用者帳戶的安全性認證。 指定的認證將用於處理、ROLAP 查詢、非正規繫結、本機 Cube、採礦模型、遠端資料分割、連結物件以及從目標到來源的同步處理。 但如果是資料採礦延伸模組 (DMX) OPENQUERY 陳述式，將忽略這個選項，而且會使用目前使用者的認證。  
  
 **使用者名稱**  
 輸入選定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件所要使用之使用者帳戶的網域和名稱。 請使用下列格式：  
  
 *\<Domain name>* **\\** *\<User account name>*  
  
 唯有選取 **[使用特定的使用者名稱和密碼]** 之後，才會啟用此選項。  
  
 **密碼**  
 輸入選定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件所要使用之使用者帳戶的密碼。  
  
 唯有選取 **[使用特定的使用者名稱和密碼]** 之後，才會啟用此選項。  
  
 **使用服務帳戶**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用與管理該物件之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服務相關聯的安全性認證。 服務帳戶認證將用於處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理。 但如果是資料採礦延伸模組 (DMX) OPENQUERY 陳述式、本機 Cube 和採礦模型，將會使用目前使用者的認證。 非正規 (out-of-line) 繫結不支援此選項。  
  
 **使用目前使用者的認證**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用目前使用者的安全性認證來進行非正規 (out-of-line) 繫結、DMX OPENQUERY、本機 Cube 和採礦模型。 處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理不支援此選項。  
  
 **都會**  
 選取此選項可使用定義於資料庫層級的模擬行為，伺服器管理員已經使用 `DataSourceImpersonation` 資料庫屬性來設定此行為。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [&#40;SSAS 多維度&#41;支援的資料來源](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
