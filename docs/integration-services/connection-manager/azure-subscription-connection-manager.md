---
description: Azure 訂用帳戶連線管理員
title: Azure 訂用帳戶連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 277e92a906acb89960e16c941fbd71df023ddb23
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678997"
---
# <a name="azure-subscription-connection-manager"></a>Azure 訂用帳戶連線管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Azure 訂用帳戶連線管理員** 可使用您指定的屬性值，即 Azure 訂用帳戶識別碼和管理憑證，讓 SSIS 封裝連接到 Azure 訂用帳戶。  
  
 **Azure 訂用帳戶連線管理員** 是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。
  
1.  在上方顯示的 [加入 SSIS 連線管理員] 對話方塊中，選取 [Azure 訂用帳戶]，然後按一下 [加入]。  [Azure Subscription Connection Manager Editor (Azure 訂用帳戶連線管理員編輯器)] 對話方塊應會隨即出現。  
  
    ![顯示 [Azure 訂用帳戶連線管理員編輯器] 對話方塊的螢幕擷取畫面。](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  在 [Azure 訂用帳戶識別碼] 輸入可唯一識別 Azure 訂用帳戶的 Azure 訂用帳戶識別碼。  可以在 [設定] 頁面下的 [Azure 管理入口網站](https://manage.windowsazure.com)找到此值：  
  
    ![在 Azure 管理入口網站中，顯示 [設定] 頁面內 [訂閱] 索引標籤的螢幕擷取畫面。](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  從下拉式清單中選擇 [Management certificate store location (管理憑證存放區位置)] 和 [Management certificate store name (管理憑證存放區名稱)]。  
  
4.  輸入 [管理憑證指紋]，或按一下 [瀏覽...] 可從選取的存放區選擇憑證。 憑證必須上傳為訂用帳戶的管理憑證。 若要這樣做，請按一下 Azure 入口網站下一個頁面上的 [上傳] (如需詳細資訊，請參閱此 [MSDN 文章](/previous-versions/azure/gg551722(v=azure.100)))。  
  
     ![在 Azure 管理入口網站中，顯示 [設定] 頁面內 [管理憑證] 索引標籤的螢幕擷取畫面。](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  按一下 [測試連接] 來測試連接。  
  
6.  按一下 **[確定]** ，關閉對話方塊。  
  
