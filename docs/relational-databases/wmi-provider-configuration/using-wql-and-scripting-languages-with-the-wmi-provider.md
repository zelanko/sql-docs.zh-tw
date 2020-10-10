---
title: 使用 WQL 和腳本存取 WMI 提供者
description: 瞭解如何使用 WQL 編輯器或查詢工具或指令碼語言，存取使用 WMI 提供者的 SQL Server 服務和網路設定。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 52bc3bc300b1f6412ba2a4cdd3ce55ba5ca93aee
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891248"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>搭配 WMI 提供者使用 WQL 與指令碼語言
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  管理應用程式會以兩種方式，使用組態管理物件的 Windows Management Instrumentation (WMI) 提供者，存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務與網路設定：  
  
-   使用 WQL 編輯器或查詢工具 (例如，WBEMTest.exe) 來查訊利用 Windows Management Instrumentation 語言 (WQL) 設定的物件。  
  
-   使用指令碼語言，例如 VBScript。  
  
 或者，可以使用 SMO 中的 WMI Managed 物件，以程式設計方式管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務與網路設定。 如需有關程式設計 WMI 受管理物件的詳細資訊，請參閱 [使用 Wmi 提供者管理服務和網路設定](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
 組態管理的 WMI 提供者可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 來進行存取。 如需從使用者介面存取 WMI 提供者的詳細資訊，請參閱 [管理服務的 how To 主題 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 WQL 存取設定管理的 WMI 提供者](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [使用 VBScript 存取 WMI 提供者](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
