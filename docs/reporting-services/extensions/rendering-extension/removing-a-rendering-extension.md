---
title: "移除轉譯延伸模組 |Microsoft 文件"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 38
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 58e9d46c17b300cda365e8b42d6442e00ffab0b9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="removing-a-rendering-extension"></a>移除轉譯延伸模組
  若要移除[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]轉譯延伸模組，只要移除**延伸**從 rsreportserver.config 檔案，位於您轉譯延伸模組項目**%ProgramFiles%\Microsoft SQL server\msrs10_50.<instancename>\reporting。\<執行個體名稱 > services\reportserver**資料夾。 如果您對報表設計工具，以及報表伺服器項目，移除**延伸**項目從[RSReportDesigner Configuration File](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md)以及。 在移除組態資訊之後，轉譯延伸模組將無法再供元件使用。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [實作轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [轉譯延伸模組概觀](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [實作 IRenderingExtension 介面](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [擴充功能的安全性考量](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [部署轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
