---
title: 建立知識庫
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: swinarko
ms.author: sawinark
ms.openlocfilehash: aa740172957e3f0ba08812e298db5621ba43e890
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887987"
---
# <a name="create-a-knowledge-base"></a>建立知識庫

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  本主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中建立知識庫，並預備此知識庫進行定義域管理、知識探索或是加入比對原則。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要建立知識庫，您必須已經安裝 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 和 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_administrator 角色，才能建立知識庫。  
  
##  <a name="create-a-knowledge-base"></a><a name="Createaknowledgebase"></a>建立知識庫  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，按一下 **[新增知識庫]**。  
  
3.  輸入新知識庫的名稱和描述。  
  
4.  在 **[建立知識庫來源]** 中，選取要做為知識庫基礎的來源：  
  
    -   如果您不想要使用現有的知識庫或資料檔案做為新知識庫的基礎，請選取 **[無]** 。  
  
    -   若要使用已經在 **上建立的知識庫或預設知識庫做為新知識庫的基礎，請選取** [現有知識庫] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。 從 **[選取知識庫]** 下拉式清單中選取知識庫，或按一下 **[瀏覽]** 顯示 **[選取知識庫]** 對話方塊、選取要做為新知識庫基礎的現有知識庫，然後按一下 **[確定]**。 當您從資料表中選取知識庫時，該知識庫的定義域和比對規則就會顯示在對話方塊的右窗格中。 您也可以選取 [DQS 資料] **** 知識庫，這是預設知識庫，其中包含與美國公司、地址和政黨資料有關的一般現成定義域及知識。  
  
    -   選取 **[從 DQS 檔案匯入]** ，即可使用 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上的 DQS 檔案做為新知識庫的基礎。 按一下 **[瀏覽]**、選取副檔名為 .dqs 的 DQS 資料檔案，然後按一下 **[確定]**。  
  
5.  在 **[選取活動]** 中，選取您想要在新知識庫上執行的活動：  
  
    -   選取 **[定義域管理]** 建立知識庫，並且進入用來修改知識庫中定義域的畫面。  
  
    -   選取 **[知識探索]** 建立知識庫，並且進入用來分析資料樣本並以結果擴展知識庫定義域的精靈。  
  
    -   選取 **[比對原則]** 建立比對原則，並將其加入至知識庫。  
  
6.  按一下 [建立]。  
  
##  <a name="follow-up-after-creating-a-knowledge-base"></a><a name="FollowUp"></a> 後續操作：建立知識庫之後  
 建立知識庫之後，系統會顯示可用來執行知識探索的精靈、建立比對原則的精靈或是執行定義域管理的頁面。 如需有關知識探索、定義域管理或比對原則的詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)或[建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
  
