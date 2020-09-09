---
title: 使用 WQL 存取 WMI 提供者
description: 使用此範例來瞭解如何針對 WMI 提供者執行 SQL Server 中電腦管理的 Windows Management Instrumentation 查詢語言語句。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 27b03d13ede2b861f90e194e4939e8c9c77ecafb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542742"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>使用 WQL 存取組態管理的 WMI 提供者
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本節描述如何針對電腦管理的 WMI 提供者執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation 查詢語言 (WQL) 陳述式。  
  
 此範例使用 WQL 編輯器 WBEMtest.exe 來針對 WMI 提供者執行 WQL 查詢，以列舉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路通訊協定和別名。  
  
### <a name="querying-services-using-wbemtest"></a>使用 WBEMtest 查詢服務  
  
1.  在 [ **開始** ] 功能表中，按一下 [ **執行**]，然後輸入 **WBEMtest**。  
  
2.  [WBEMtest.exe] 對話方塊隨即出現。 按一下 [連線]。  
  
3.  在第一個文字欄位中，輸入電腦管理的 WMI 提供者命名空間：root\Microsoft\SqlServer\ComputerManagement11。 按一下 [連線]。  
  
4.  按一下 **[查詢]**。 輸入會傳回目前在本機電腦上執行之服務的查詢： **SELECT \* FROM SqlService。** 按一下 [套用]。  
  
5.  藉由新增 **WHERE ServiceName = "MSSQLSERVER"** 來進一步精簡查詢。  
  
  
