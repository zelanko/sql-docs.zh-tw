---
title: 執行 Data Quality Client 應用程式
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 7179387d5ae3d2dd045332d0dd5d0fad7fcdebd8
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813763"
---
# <a name="run-the-data-quality-client-application"></a>執行 Data Quality Client 應用程式

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  執行 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]並登入 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 您必須執行 DQSInstaller.exe 檔案，才可以完成 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 的安裝。 如需詳細資訊，請參閱 [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有授與 DQS_MAIN 資料庫的其中一個 DQS 角色 (dqs_adminstrator、dqs_kb_editor 或 dqs_kb_operator)，才能登入 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
##  <a name="run-data-quality-client"></a><a name="Run"></a>執行 Data Quality Client  
 若要在已安裝 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的電腦上執行它，請：  
  
1.  按一下 [開始]****，並指向 [所有程式]****，然後依序按一下 [[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]]****、[Data Quality Services]**** 及 [Data Quality Client]****。  
  
2.  在 **[連接到伺服器]** 對話方塊中：  
  
    1.  指定您想要讓 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式連接的目標伺服器。 若要連接到本機電腦上的 **，請選取** [(LOCAL)] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 。 您也可以按一下向下箭號，然後選取 **\<Browse network for more servers>** 以連接到不同的伺服器（或依名稱連接到本機伺服器）。 此時會顯示 **[瀏覽伺服器]** 對話方塊。 您可以在 **[本機伺服器]** 索引標籤或 **[網路伺服器]** 索引標籤中選取伺服器。  
  
    2.  加密 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 與 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]之間的資料傳輸，按一下 [選項] ****，然後選取 [加密連接] **** 核取方塊。  
  
3.  按一下 [ **連接**]。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面隨即出現。 如需詳細資訊，請參閱 [Data Quality Client 首頁畫面](../data-quality-services/data-quality-client-home-screen.md)。  
  
  
