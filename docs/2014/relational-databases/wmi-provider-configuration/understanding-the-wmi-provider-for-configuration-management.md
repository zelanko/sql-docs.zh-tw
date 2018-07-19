---
title: 了解組態管理的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
caps.latest.revision: 20
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d4917968888760b0910629338eb435df41769efc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222918"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>了解用於組態管理的 WMI 提供者
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供用於組態管理的 WMI 提供者。 這可讓您使用 Windows Management Instrumentation (WMI) 管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端與伺服器的網路設定，以及伺服器別名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、 網路設定與別名會以 WMI 物件表示在 root\Microsoft\SqlServer\ComputerManagement*nn*命名空間的電腦。 在指定的電腦上建立與 WMI 提供者的連接之後，可以使用 WQL 或指令碼語言查詢服務、網路設定與別名。  
  
 WMI 提供者是執行個體提供者。 它提供的執行個體[WMI 類別](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)並支援下列非同步作業。  
  
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
  
 如需使用組態管理的 WMI 提供者的管理應用程式的範例，請參閱[使用 WQL 與指令碼與組態管理的 WMI 提供者的語言](using-wql-and-scripting-languages-with-the-wmi-provider.md)。  
  
 如需有關如何使用 WMI 提供者的管理應用程式的程式設計的詳細資訊，請參閱 WMI 文件中的[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework SDK。  
  
## <a name="see-also"></a>另請參閱  
 [使用組態管理的 WMI 提供者](working-with-the-wmi-provider-for-configuration-management.md)   
 [搭配組態管理的 WMI 提供者使用 WQL 與指令碼語言](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
