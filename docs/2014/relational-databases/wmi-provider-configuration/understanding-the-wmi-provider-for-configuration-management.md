---
title: 瞭解設定管理的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a2ecd601b1329b3b95f1c3827cd04775c93304f6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061274"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>了解用於組態管理的 WMI 提供者
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供設定管理的 WMI 提供者。 這可讓您使用 Windows Management Instrumentation (WMI) 管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端與伺服器的網路設定，以及伺服器別名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務、網路設定和別名是由電腦的 root\Microsoft\SqlServer\ComputerManagement*nn*命名空間中的 WMI 物件所代表。 在指定的電腦上建立與 WMI 提供者的連接之後，可以使用 WQL 或指令碼語言查詢服務、網路設定與別名。  
  
 WMI 提供者是執行個體提供者。 它會提供[WMI 類別](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)的實例，並支援下列非同步作業。  
  
 執行個體擷取  
 擷取特定類別類型執行個體。  
  
 列舉型別  
 列舉類別類型的所有執行個體。  
  
 修改  
 修改類別類型的特定執行個體。  
  
 類別所擁有的方法允許修改其屬性。  
  
 刪除  
 移除類別類型的特定執行個體。  
  
 查詢處理  
 根據篩選器列舉類別類型的執行個體。  
  
 如需使用 WMI 提供者進行設定管理的管理應用程式範例，請參閱搭配[Wmi 提供者使用 WQL 和指令碼語言來進行設定管理](using-wql-and-scripting-languages-with-the-wmi-provider.md)。  
  
 如需有關使用 WMI 提供者進行程式設計管理應用程式的詳細資訊，請參閱 .NET Framework SDK 中的 WMI 檔 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [使用 WMI 提供者進行設定管理](working-with-the-wmi-provider-for-configuration-management.md)   
 [搭配組態管理的 WMI 提供者使用 WQL 與指令碼語言](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
