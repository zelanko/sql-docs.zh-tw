---
title: 設定清理和比對的閾值 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dbb09e9aa932797a975f26de15e2b466101c4026
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616308"
---
# <a name="configure-threshold-values-for-cleansing-and-matching"></a>設定清理和比對的臨界值

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  此主題描述如何設定臨界值，該值將會在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的電腦輔助的清理和比對活動期間使用。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_administrator 角色，才能設定這些臨界值。  
  
##  <a name="Configure"></a> 設定臨界值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[組態]**。  
  
3.  接下來，按一下 **[一般設定]** 索引標籤。此索引標籤可讓您針對清理和比對活動指定臨界值。  
  
4.  若要針對清理活動指定臨界值，請在 **[互動式清理]** 區域的以下方塊中指定適當的值：  
  
    -   **建議的最低分數**：DQS 在電腦輔助的清理程序期間將用來建議某個值之取代的最低分數或信賴等級。 請使用對應百分比值的十進位表示法來輸入值。 例如，輸入 0.75 代表 75%。 這個值應該要小於或等於 **[自動更正的最低分數]** 方塊中指定的值。 預設值為 0.7。  
  
    -   **自動更正的最低分數**：DQS 在電腦輔助的清理程序期間將用來自動更正某個值的最低分數或信賴等級。 請使用對應百分比值的十進位表示法來輸入值。 例如，輸入 0.9 表示 90%。 預設值為 0.8。  
  
5.  若要針對比對活動指定臨界值，請在 **[比對]** 區域底下的 **[最低記錄分數]** 方塊中指定值。 這個值表示讓某筆記錄被視為符合另一筆記錄的最低分數。 預設值是 80%。  
  
6.  按一下 [ **關閉**]。  
  
  
