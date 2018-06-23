---
title: Azure 儲存體連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 41ddc29a865b84ef01721931b0702476fe6b9ec1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145893"
---
# <a name="azure-storage-connection-manager"></a>Azure 儲存體連線管理員
  Azure 儲存體連接管理員可讓 SSIS 封裝連接到 Azure 儲存體帳戶所使用的屬性所指定的值： 儲存體帳戶名稱和帳戶金鑰。  
  
1.  在 [加入 SSIS 連線管理員] 對話方塊中，選取 [AzureStorage]，然後按一下 [加入]。  
  
2.  在 [Azure 儲存體連線管理員編輯器] 對話方塊中，選擇 [使用 Azure 帳戶] 透過網際網路連接至 Azure 儲存體服務，或選擇 [使用本機開發人員帳戶] 連接至 Azure 儲存體模擬器裝載的本機服務。  
  
3.  如已選取 [使用 Azure 帳戶] 選項，請執行下列動作︰  
  
    1.  指定 [儲存體帳戶名稱] 和 [帳戶金鑰] 欄位的值。 這些值會儲存為 SSIS 封裝中的機密資料。  
  
    2.  如果您想要使用 HTTPS 而非 HTTP連接到 Azure 儲存體服務，請選取 [使用 HTTPS]。  
  
4.  按一下 **[確定]** ，關閉對話方塊。  
  
5.  您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。  
  
  