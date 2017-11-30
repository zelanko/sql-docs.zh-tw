---
title: "移除轉譯延伸模組 | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: "38"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7603ca8ad7e5fb5688b51e847a7b742cf691afb1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="removing-a-rendering-extension"></a>移除轉譯延伸模組
  若要移除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 轉譯延伸模組，只要從 rsreportserver.config 檔案 (位於 **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<執行個體名稱>\Reporting Services\ReportServer** 資料夾) 中移除轉譯延伸模組的 **Extension** 項目即可。 如果您已經為報表設計師以及報表伺服器建立項目，請同時從 [RSReportDesigner 設定檔](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md)中移除 **Extension** 項目。 在移除組態資訊之後，轉譯延伸模組將無法再供元件使用。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [實作轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [轉譯延伸模組概觀](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [實作 IRenderingExtension 介面](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [延伸模組的安全性考量](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [部署轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
