---
title: 設定 DQS 使用參考資料
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.rdsconfiguration.f1
- sql13.dqs.administration.configuration.createDirectRDS.f1
- sql13.dqs.admin.config.rds.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 542e32606858604e59cdbf204bbf39eba6d214a6
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813862"
---
# <a name="configure-dqs-to-use-reference-data"></a>設定 DQS 使用參考資料

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  此主題描述如何設定 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 來使用參考資料清理您的資料。 您可以使用來自 Azure Marketplace 的參考資料，或從直接線上協力廠商參考資料提供者。  

> [!IMPORTANT]
> 本文提到的協力廠商參考資料服務先前可從 Azure DataMarket 取得。 自 2016 年 12 月 31 日起已中止 DataMarket 和資料服務 (例如包含 Melissa 位址資料)。 因此，您再也無法使用從 DataMarket 取得的指定服務來執行本文中的範例。 但您仍然可以使用協力廠商參考資料提供者直接線上提供的參考資料服務。

## <a name="before-you-begin"></a>開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要使用服務商場的參考資料，您必須擁有有效的服務商場帳號金鑰。 如需有關建立 Marketplace 帳戶金鑰的詳細資訊，請參閱[建立您的帳戶](https://go.microsoft.com/fwlink/?LinkId=212936)（ https://go.microsoft.com/fwlink/?LinkId=212936) 。 您也可以從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 建立服務商場帳號金鑰，方法是按一下 **首頁畫面中** [管理] **底下的** [組態] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ，然後按一下 **[參考資料]** 索引標籤底下的 **[建立 DataMarket 帳戶識別碼]** 。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_administrator 角色，才能在 DQS 中設定參考資料服務。  
  
##  <a name="configure-dqs-to-use-reference-data-from-marketplace"></a><a name="Marketplace"></a> 設定 DQS 使用服務商場中的參考資料  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[管理]** 底下的 **[組態]**。  
  
3.  在 **[參考資料]** 索引標籤的 **[網路設定]** 區域底下，於 **[Proxy 伺服器]** 和 **[通訊埠]** 方塊中輸入適當的值 (如果您或您的組織使用 Proxy 伺服器連接至網際網路)。  
  
4.  在 **[DataMarket 帳戶識別碼]** 方塊中指定服務商場帳號金鑰，然後按一下 **[驗證 DataMarket 帳戶識別碼]** 圖示來驗證此帳號金鑰。 隨即出現一則訊息，顯示指定的服務商場帳號金鑰是否有效。  
  
 您現在已經準備好開始在 DQS 中使用來自服務商場的參考資料服務 (這些服務是針對指定的服務商場帳號金鑰所訂閱)。  
  
##  <a name="configure-dqs-to-use-reference-data-from-direct-online-third-party-reference-data-providers"></a><a name="ThirdParty"></a> 設定 DQS 使用直接線上協力廠商參考資料提供者所提供的參考資料  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[管理]** 底下的 **[組態]**。  
  
3.  在 **[參考資料]** 索引標籤的 **[網路設定]** 區域底下，於 **[Proxy 伺服器]** 和 **[通訊埠]** 方塊中輸入適當的值 (如果您或您的組織使用 Proxy 伺服器連接至網際網路)。  
  
4.  在 **[直接線上協力廠商參考資料服務設定]** 區域中按一下 **[加入新的參考資料服務提供者]** 圖示。  
  
5.  在 **[建立新的直接線上協力廠商參考資料服務提供者]** 對話方塊中，指定以下詳細資料：  
  
    1.  在 **[名稱]** 方塊中，輸入新的直接參考資料服務提供者的名稱。  
  
    2.  (選擇性) 在 **[描述]** 方塊中，輸入新的直接參考資料服務提供者的描述。  
  
    3.  在 **[類別目錄]** 方塊中，輸入新的直接參考資料服務提供者所提供之資料的類別目錄。  
  
    4.  在 [結構描述] 方塊中，指定可定義要從直接參考資料服務提供者使用之欄位字串 (資料行名稱) 的結構描述。 欄位名稱不能包含空格，而且應該以逗號分隔欄位。 例如：`FirstName, LastName, City, State`。  
  
    5.  在 **[URI]** 方塊中，輸入直接參考資料服務提供者的 URI。 DQS 中只允許安全的 URI (以 "https://" 開頭的位址)。  
  
    6.  在 **[最大批次大小]** 方塊中，輸入將傳送給參考資料服務提供者進行清理之每個批次的最大記錄數目。 每個批次最多可以針對清理活動指定 100 筆記錄。  
  
    7.  在 **[帳戶識別碼]** 方塊中，輸入參考資料服務提供者之訂閱者的帳戶識別碼。  
  
6.  按一下 **[確定]** 儲存資料，並關閉 **[建立新的直接線上協力廠商參考資料服務提供者]** 對話方塊。 新加入的直接線上協力廠商參考資料提供者便可以在 DQS 中的 **[直接參考資料服務提供者]** 方格內使用。  
  
 您現在已經準備好開始在 DQS 中使用來自新設定的直接線上協力廠商參考資料服務提供者所提供的參考資料服務。  
  
##  <a name="follow-up-after-configuring-dqs-to-use-reference-data"></a><a name="FollowUp"></a>後續操作：設定 DQS 使用參考資料之後  
 您現在必須將必要的知識庫定義域對應到您剛才設定的資料提供者所提供的參考資料。 若要如此做，請參閱[將定義域或複合定義域附加至參考資料](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)。  
  
  
