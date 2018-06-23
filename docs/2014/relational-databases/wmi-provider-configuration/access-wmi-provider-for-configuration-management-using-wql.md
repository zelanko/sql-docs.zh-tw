---
title: 存取 WMI 提供者使用 WQL 的組態管理 |Microsoft 文件
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
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c3c9ced24edc7e7f3537a73d074cf7cd73128dc8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031835"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>使用 WQL 存取組態管理的 WMI 提供者
  本節描述如何針對電腦管理的 WMI 提供者執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation 查詢語言 (WQL) 陳述式。  
  
 此範例使用 WQL 編輯器 WBEMtest.exe 來針對 WMI 提供者執行 WQL 查詢，以列舉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路通訊協定和別名。  
  
### <a name="querying-services-using-wbemtest"></a>使用 WBEMtest 查詢服務  
  
1.  從**啟動**功能表上，按一下 **執行**，然後輸入`WBEMtest`。  
  
2.  [WBEMtest.exe] 對話方塊隨即出現。 按一下 **[連接]**。  
  
3.  在第一個文字欄位中，輸入電腦管理的 WMI 提供者命名空間：root\Microsoft\SqlServer\ComputerManagement11。 按一下 **[連接]**。  
  
4.  按一下**查詢**。 輸入查詢，以傳回本機電腦上執行的目前服務：**選取\*從 SqlService。** 按一下 **[套用]**。  
  
5.  加入 `WHERE ServiceName = "MSSQLSERVER"` 來進一步精簡查詢。  
  
  