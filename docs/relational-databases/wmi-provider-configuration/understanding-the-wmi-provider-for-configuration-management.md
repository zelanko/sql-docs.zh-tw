---
title: 組態管理的 WMI 提供者
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 21ca5f7039b11b30c11a0fb707f6b6e89244bae2
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658910"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>了解用於組態管理的 WMI 提供者
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供設定管理的 WMI 提供者。 這可讓您使用 Windows Management Instrumentation (WMI) 管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端與伺服器的網路設定，以及伺服器別名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路設定和別名是由電腦的 root\Microsoft\SqlServer\ComputerManagement*nn*命名空間中的 WMI 物件所代表。 在指定的電腦上建立與 WMI 提供者的連接之後，可以使用 WQL 或指令碼語言查詢服務、網路設定與別名。  
  
 WMI 提供者是執行個體提供者。 它會提供[WMI 類別](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)的實例，並支援下列非同步作業。  
  
 執行個體擷取  
 擷取特定類別類型執行個體。  
  
 {1}列舉型別{2}  
 列舉類別類型的所有執行個體。  
  
 修改  
 修改類別類型的特定執行個體。  
  
 類別所擁有的方法允許修改其屬性。  
  
 刪除  
 移除類別類型的特定執行個體。  
  
 查詢處理  
 根據篩選器列舉類別類型的執行個體。  
  
 如需使用 WMI 提供者進行設定管理的管理應用程式範例，請參閱搭配[Wmi 提供者使用 WQL 和指令碼語言來進行設定管理](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)。  
  
 如需有關使用 WMI 提供者進行程式設計管理應用程式的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK 中的 WMI 檔。  
  
## <a name="see-also"></a>另請參閱  
 使用設定[管理  的 WMI 提供者](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)  
 [搭配組態管理的 WMI 提供者使用 WQL 與指令碼語言](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
