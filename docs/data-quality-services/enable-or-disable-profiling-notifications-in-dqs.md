---
description: 在 DQS 中啟用或停用分析通知
title: 在 DQS 中啟用或停用分析通知
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- enable notifications
- notifications,enable
- notifications,disable
ms.assetid: e439bb29-60cc-4afd-a79a-f629b8d843c1
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4595f034ad1a3c26f3991af21207bb02e4321769
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431310"
---
# <a name="enable-or-disable-profiling-notifications-in-dqs"></a>在 DQS 中啟用或停用分析通知

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中啟用或停用分析通知。 根據預設，DQS 中會啟用分析通知。 分析通知告訴您有關資料來源的重要事實，以及針對資料執行之目前活動的效用。 如需詳細資訊，請參閱 [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md)。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_administrator 角色，才能啟用通知。  
  
##  <a name="enable-or-disable-profiling-notifications"></a><a name="Enable"></a> 啟用或停用分析通知  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[組態]**。  
  
3.  接下來，按一下 **[一般設定]** 索引標籤。  
  
4.  清除或選取 **[啟用通知]** 核取方塊，針對 DQS 中的各種活動啟用分析通知。  
  
5.  按一下 [關閉] 。  
  
  
