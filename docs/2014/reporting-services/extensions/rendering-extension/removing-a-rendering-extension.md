---
title: 移除轉譯延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 77a8a9ac44b35f338f978913985617e4f264ddb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62988057"
---
# <a name="removing-a-rendering-extension"></a>移除轉譯延伸模組
  若要移除[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]轉譯延伸模組，請直接`Extension`從位於 **%ProgramFiles%\Microsoft SQL Server \ MSRS10_50 的 rsreportserver.config 中移除轉譯延伸模組的元素。\<實例名稱> \Reporting Services\ReportServer**資料夾。 如果您是報表設計師和報表伺服器的專案，請一併移除`Extension` [rsreportdesigner.config 設定檔](../../report-server/rsreportdesigner-configuration-file.md)中的元素。 在移除組態資訊之後，轉譯延伸模組將無法再供元件使用。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](../../report-server/reporting-services-configuration-files.md)   
 [實作轉譯延伸模組](implementing-a-rendering-extension.md)   
 [轉譯延伸模組概觀](rendering-extensions-overview.md)   
 [實作 IRenderingExtension 介面](implementing-the-irenderingextension-interface.md)   
 [延伸模組的安全性考量](../security-considerations-for-extensions.md)   
 [部署轉譯延伸模組](deploying-a-rendering-extension.md)  
  
  
